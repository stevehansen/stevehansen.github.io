---
title: Rails dynamic finders for .NET 4.0
author: Steve Hansen
layout: post
permalink: /2010/06/19/rails-dynamic-finders-for-net-40/
---
Ruby on Rails allows you to use &#8216;dynamic&#8217; finders to query the database. This is actually a feature from ActiveRecord to dynamicly use methods which will represent where clauses on the database.

Some examples:

<pre class="brush: ruby">User.find(:first, :conditions =&gt; ["name = ?", name])
User.find_by_name(name)

User.find(:all, :conditions =&gt; ["city = ?", city])
User.find_all_by_city(city)

User.find(:all, :conditions =&gt; ["street = ? AND city IN (?)", street, cities])
User.find_all_by_street_and_city(street, cities)</pre>

With .NET 4.0 we have dynamics of our own so I thought why not recreate this feature&#8230;

By creating an extension method for IEnumerable<T> and IQueryable<T> each enumerable source can now use the dynamic finder feature

<pre class="brush: csharp">public static class DynamicExtensions
{
    public static dynamic AsDynamic&lt;T&gt;(this IEnumerable&lt;T&gt; source)
    {
        return new DynamicEnumerable&lt;T&gt;(source);
    }

    public static dynamic AsDynamic&lt;T&gt;(this IQueryable&lt;T&gt; source)
    {
        return new DynamicQueryable&lt;T&gt;(source);
    }
}</pre>

The Dynamic classes will inherit from DynamicObject to give basic dynamics support.

<pre class="brush: csharp">sealed class DynamicQueryable&lt;T&gt; : DynamicObject
{
    private readonly IQueryable&lt;T&gt; source;

    public DynamicQueryable(IQueryable&lt;T&gt; source)
    {
        this.source = source;
    }

    public override bool TryInvokeMember(InvokeMemberBinder binder, object[] args, out object result)
    {
        var match = methodMatcher.Match(binder.Name);
        if (match.Success)
        {
            var properties = match.Groups[2].Value.Split(new[] { "And" }, StringSplitOptions.RemoveEmptyEntries);
            var predicate = BuildExpression&lt;T&gt;(properties, args);

            if (match.Groups[1].Success)
                result = source.Where(predicate);
            else
                result = source.FirstOrDefault(predicate);

            return true;
        }
        return base.TryInvokeMember(binder, args, out result);
    }
}</pre>

With the only missing part the BuildExpression method which will create the expression tree:

<pre class="brush: csharp">private static Expression&lt;Func&lt;T, bool&gt;&gt; BuildExpression&lt;T&gt;(string[] properties, object[] args)
{
    if (properties.Length &lt; 1)
       throw new InvalidOperationException("Need to specify at least one property.");
    if (args.Length != properties.Length)
       throw new InvalidOperationException("Method expects " + properties.Length + " parameters and only got " + args.Length + " values.");

    var param = Expression.Parameter(typeof(T), "p");
    var body = Expression.Equal(Expression.Property(param, properties[0]), Expression.Constant(args[0]));
    for (var i = 1; i &lt; properties.Length; i++)
        body = Expression.AndAlso(body, Expression.Equal(Expression.Property(param, properties[i]), Expression.Constant(args[i])));
    return Expression.Lambda&lt;Func&lt;T, bool&gt;&gt;(body, param);
}</pre>

And the only difference with the DynamicEnumerable class is that the expression will be compiled to use for the Where/FirstOrDefault.

Full source at [pastebin][1].


 [1]: http://pastebin.com/m6FmvUGj "http://pastebin.com/m6FmvUGj"