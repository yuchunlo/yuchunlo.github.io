---
layout: default
permalink: /tags/
---

{% capture site_tags %}{% for tag in site.tags %}{{ tag | first }}{% unless forloop.last %},{% endunless %}{% endfor %}{% endcapture %}
{% assign site_tags_sorted = site_tags | split:',' | sort %}

<div> | 
{% for tag in site_tags_sorted %}
  <a href='/blog/#{{ tag | slugify }}'>{{ tag | strip_newlines }}</a> | 
{% endfor %}
</div>

{% for tag in site_tags_sorted %}
  <div name='{{ tag | slugify }}'>
    <button class='tag'>{{ tag }}</button><br>
    {% for post in site.tags[tag] %}
      <div id='date'>{{ post.date | date: '%-d %B, %Y' }}</div>
      <div id='page-title'><a href='{{ post.url }}'>{{ post.title }}</a></div>
      {{ post.content | truncatewords: 50 | strip_html | xml_escape }}
      <a href='{{ post.url }}'>[Read&nbsp;More]</a>
      <br><br><br>
    {% endfor %}
  </div>
{% endfor %}
