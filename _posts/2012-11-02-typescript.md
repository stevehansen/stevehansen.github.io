---
title: TypeScript
author: Steve Hansen
layout: post
permalink: /2012/11/02/typescript/
tags:
  - JavaScript
  - TypeScript
---
Finally got some time to check out TypeScript. The first impressions are good, all current JavaScript is automatically valid TypeScript! This allows you to easily update existing JavaScript code step by step.

The resulting generated JavaScript is also easy read which is a plus. And if you would ever have a problem (not supported anymore, blocking bug, &#8230;) you can just use the latest generated .js and work from there.

Gives the same impression as less and we use that one too for building our styles.

{% highlight ts %}interface Person {
    firstname: string;
    lastname: string;
}

function greeter(person : Person) {
    return "Hello, " + person.firstname + " " + person.lastname;
}

var user = {firstname: "Jane", lastname: "User"};

document.body.innerHTML = greeter(user);{% endhighlight %}

This is the feature I like most, duck typing at its core. Just define what you are expecting and the compiler will check this for you. The Microsoft TFS team converted their web client to use TypeScript and already fixed 13 bugs that they didn&#8217;t know existed before, while they still have unit tests, integration tests and no jslint errors.

More info: <http://www.typescriptlang.org/> (with a play ground in the browser)