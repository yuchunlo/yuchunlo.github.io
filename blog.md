---
layout: default
title: Blog
permalink: /blog/
---

{% for post in paginator.posts %}
  <div id="date">{{ post.date | date: "%-d %B, %Y" }}</div>
  <a href="{{ post.url | prepend: site.baseurl }}">
	  <div id="page-title">{{ post.title }}</div>
  </a>
  {{ post.content | truncatewords: 50 | strip_html | xml_escape}}
  <a href="{{ post.url | prepend: site.baseurl }}">[Read&nbsp;More]</a>
{% endfor %}
