---
layout: default
title: Home
tagline: Welcome to Salil's Mind Palace!
keywords: Salil, Salil Dabholkar, Salil Blog, machine learning, research
---

# Publications
<!-- ACM DL Article: Automatic Document Summarization using Sentiment Analysis -->
<div class="acmdlitem" id="item2980362" style="margin-bottom: 15px"><a href="https://dl.acm.org/authorize?N27517" title="Automatic Document Summarization using Sentiment Analysis">Automatic Document Summarization using Sentiment Analysis</a><div><a href="http://dl.acm.org/author_page.cfm?id=99659084760" >Salil Dabholkar</a>, <a href="http://dl.acm.org/author_page.cfm?id=99659083162" >Yuvraj Patadia</a>, <a href="http://dl.acm.org/author_page.cfm?id=99659083680" >Prajyoti Dsilva</a><br />Proceedings of the International Conference on Informatics and Analytics (ICIA-16). ACM, New York, NY, USA.</div></div>

My first research effort focused on developing a novel mechanism for automatically creating summaries of textual documents.
I found a way to use sentiment analysis along with appropriate fallback mechanisms to achieve the needed results.


# Projects

|--------------+------------+-----------------+----------------|
|    Project   | Description                                                                                                                                                                                      | Example Output                                                      | Links                  |
|:------------:|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------|------------------------|
| Game of Life using Deep Neural Net | Created a neural net to simulate [Conway's Game of Life](https://en.wikipedia.org/wiki/Conway%27s_Game_of_Life). Learns to generate the next state from any given random initial state | ![Game of Life](assets/images/GoL/life.gif "Game of Life in action")  | [[code](https://github.com/salildabholkar/Deep-Learning/tree/master/GameOfLife)], [[blog]()] |
| Deep Song | A deep learning based generator|   | [[code]()], [[blog]()] |
|--------------+------------+-----------------+----------------|


# Top Blogs
<div class="posts">
  
  <h2>Paper summary series</h2>
  I have been keeping a personal summary of interesting papers I read
  for my future self to look back and review them without having to
  read them all over again. I have put some of the interesting ones on my website:
  
  <ul>
      {% for post in site.posts %}
        {% if post.layout == "summary" %}
            <li><a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
        {% endif %}
      {% endfor %}
  </ul>
  
  {% for post in site.posts %}
    {% if post.layout == "post" %}
        <h2><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></h2>
	    {{ post.excerpt }}
	{% endif %}
  {% endfor %}
</div>
