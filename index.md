---
layout: default
---
<div class="posts">
  {% for post in site.posts %}<article class="post">    
    <h1><a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a></h1>
	<div class="date"><time is="relative-time" datetime="{{ post.date | date_to_xmlschema }}">{{ post.date | date: "%B %e, %Y" }}</time></div>
    <div class="entry">{{ post.content | truncatewords:40}}</div>
    <a href="{{ site.baseurl }}{{ post.url }}" class="read-more">Read More</a>
  </article>{% endfor %}
</div>