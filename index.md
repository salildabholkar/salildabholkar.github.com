---
layout: page
title: Salil Dabholkar
tagline: Welcome to Salil's Mind Palace!
description: Salil Dabholkar takes you on a tour of his Mind Palace
---
{% include JB/setup %}

## About me
My name is Salil. On the internet I am known by the nicknames "UltimateSupreme" (since long ago, too long to get rid of) or "UltiSup" (much more unique). I am an aspiring Web Developer and Programmer in India.

My primary skill is solid knowledge of end-to-end web development using CSS, HTML, JavaScript and bit of PHP.
I am also good with few general purpose programming languages like C, Java and Ruby

I have very good hygiene and outstanding hair :)
I occasionally like to bake a cake.


## Research Experience
I am a budding researcher dabbling in Data Science and Artificial Intelligence. My first research effort focused on developing a novel mechanism for automatically creating summaries of documents.


## Blog Posts
<ul class="posts">
  {% for post in site.posts %}
    <h3><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></h3>
	{{ post.excerpt }}
  {% endfor %}
</ul>