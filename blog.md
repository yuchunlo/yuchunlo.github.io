---
layout: default
title: Blog
permalink: /blog/
---

{% capture site_tags %}{% for tag in site.tags %}{{ tag | first }}{% unless forloop.last %},{% endunless %}{% endfor %}{% endcapture %}
{% assign site_tags_sorted = site_tags | split:',' | sort %}

{% for tag in site_tags_sorted %}
  <a href='/blog/#{{ tag | slugify }}' style='white-space:nowrap;'>{{ tag }}</a>
{% endfor %}

{% if page.url == '/blog/' %}
  {% for post in site.posts %}
    {% if post.url != '/now/' and post.url != '/about/' and post.url != '/us/' %}
      <div id='date'>{{ post.date | date: '%-d %B, %Y' }}</div>
      <div id='page-title'><a href='{{ post.url }}'>{{ post.title }}</a></div>
      {{ post.content | truncatewords: 50 | strip_html | xml_escape }}
      <a href='{{ post.url }}'>[Read&nbsp;More]</a>
      <br><br><br>
    {% endif %}
  {% endfor %}
{% else %}
  {% for tag in site_tags_sorted %}
    <div name='{{ tag | slugify }}' style='display:none;'>
      {% for post in site.tags[tag] %}
        <div id='date'>{{ post.date | date: '%-d %B, %Y' }}</div>
        <div id='page-title'><a href='{{ post.url }}'>{{ post.title }}</a></div>
        {{ post.content | truncatewords: 50 | strip_html | xml_escape }}
        <a href='{{ post.url }}'>[Read&nbsp;More]</a>
        <br><br><br>
      {% endfor %}
    </div>
  {% endfor %}
{% endif %}
