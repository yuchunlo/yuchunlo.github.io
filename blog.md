---
layout: default
title: Blog
permalink: /blog/
---

{% for post in site.posts %}
{% if post.permalink and post.url != '/now/' and post.url != '/about/' and post.url != '/us/' %}
  <div id='date'>{{ post.date | date: '%-d %B, %Y' }}</div>
  <div id='page-title'><a href='{{ post.url }}'>{{ post.title }}</a></div>
  {{ post.content | truncatewords: 50 | strip_html | xml_escape }}
  <a href='{{ post.url }}'>[Read&nbsp;More]</a>
  <br><br><br>
{% endif %}
{% endfor %}
