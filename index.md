---
layout: page
title: Salil Dabholkar
tagline: Welcome to Salil's Mind Palace!
description: Salil Dabholkar takes you on a tour of his Mind Palace. Know more about him and his interests. Salil is an aspiring Web Developer and Programmer and is currently a student in St. Francis Institute of Technology.
keywords: Salil, Salil Dabholkar, Salil Blog, UltimateSupreme, SFIT, St. Francis Institute of Technology, Research
---
{% include JB/setup %}

## About me
My name is Salil. 
I currently work as a Web Application Developer at Media.net, 
a global leader in contextual advertising.

## Publications
<!-- ACM DL Article: Automatic Document Summarization using Sentiment Analysis -->
<div class="acmdlitem" id="item2980362"><img class="acmlogo" src="https://dl.acm.org/images/oa.gif" width="20" height="20" border="0" alt="ACM DL Author-ize service" style="vertical-align:middle"/><a href="https://dl.acm.org/authorize?N27517" title="Automatic Document Summarization using Sentiment Analysis">Automatic Document Summarization using Sentiment Analysis</a><div style="margin-left:25px"><a href="http://dl.acm.org/author_page.cfm?id=99659084760" >Salil Dabholkar</a>, <a href="http://dl.acm.org/author_page.cfm?id=99659083162" >Yuvraj Patadia</a>, <a href="http://dl.acm.org/author_page.cfm?id=99659083680" >Prajyoti Dsilva</a><br />ICIA-16 Proceedings of the International Conference on Informatics and Analytics,&nbsp;2016</div></div>

My first research effort focused on developing a novel mechanism for automatically creating summaries of textual documents.
I found a way to use sentiment analysis along with appropriate fallback mechanisms to achieve the needed results.
The paper was presented in ACM's **"INTERNATIONAL CONFERENCE ON INFORMATICS AND ANALYTICS"** and is available for reading
in the [ACM Digital Library](http://dl.acm.org).

## Projects

|--------------+------------+-----------------+----------------|
|    Project   | Description                                                                                                                                                                                      | Example Output                                                      | Links                  |
|:------------:|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------|------------------------|
| Game of Life | Meant to simulate [Conway's Game of Life](https://en.wikipedia.org/wiki/Conway%27s_Game_of_Life). Starts with a random state and sses a Deep Neural Net to automatically generate the next state | ![Game of Life](assets/images/GoL/life.gif "Game of Life in action")  | [[code]()], [[blog]()] |
|--------------+------------+-----------------+----------------|

## Top Blogs
<div class="posts">
  {% for post in site.posts %}
    <h3><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></h3>
	{{ post.excerpt }}
  {% endfor %}
</div>
