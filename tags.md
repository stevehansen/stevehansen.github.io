---
title: Tags
author: Steve Hansen
layout: page
permalink: /tags/
---
<ul>
{% for tag in site.tags %}  <li><a href="#{{ tag[0] }}">{{ tag[0] }}</a> ({{tag | last | size }})</li>
{% endfor %}</ul>
<h2>Articles by tag</h2>
<ul>{% for tag in site.tags %}
  <li><a name="{{ tag[0] }}"></a>{{ tag[0] }}
    <ul>{% for posts in tag offset: 1 %}
      {% for post in posts %}<li><a href="{{ post.url }}">{{ post.title }}</a></li>{% endfor %}
    {% endfor %}</ul>
  </li>{% endfor %}
</ul>