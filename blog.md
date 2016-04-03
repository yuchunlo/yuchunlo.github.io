---
layout: default
title: Blog
permalink: /blog/
---

{% for post in site.posts %}
  <div id="date">{{ post.date | date_to_string }}</div>
  <div id="page-title"><a href="{{ post.url }}">{{ post.title }}</a></div>
  {{ post.content | truncatewords: 50 | strip_html | xml_escape }}
  <a href="{{ post.url }}">[Read&nbsp;More]</a>
{% endfor %}
