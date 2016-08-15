---
layout: page
title: Salil Dabholkar
tagline: Welcome to Salil's Mind Palace!
---
{% include JB/setup %}

<ul class="posts">
  {% for post in site.posts %}
    <h2><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></h2>
	{{ post.excerpt }}
  {% endfor %}
</ul>