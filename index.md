---
layout: default
title: Home
tagline: Welcome to Salil's Mind Palace!
keywords: Salil, Salil Dabholkar, Salil Blog, machine learning, research
---

# Projects

|--------------+------------+-----------------+----------------|
|    Project   | Description                                                                                                                                                                                      | Example Output                                                      | Links                  |
|:------------:|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------|------------------------|
| Highway Path planner | Used a Deep Convolution Neural Net to learn features from a [German Traffic dataset](http://benchmark.ini.rub.de/?section=gtsrb&subsection=dataset). The model could then accurately classify real-world traffic sign images | ![Traffic sign](https://salildabholkar.github.io/assets/images/traffic/classification.png)  | [[blog and code](https://github.com/salildabholkar/Vision/blob/master/Traffic%20Sign%20Classifier/Traffic_Sign_Classifier.ipynb)] |
| Traffic Sign classifier | Used the car’s localization and sensor fusion data for prediction of other vehicles, decision making, and trajectory planning. <br/> Easily drove 20+ miles autonomously without accidents (required was 4mi) within the given restrictions of jerk and max speed  | ![Path planning](https://salildabholkar.github.io/assets/images/PathPlanning/res2.png)  | [[code](https://github.com/salildabholkar/Robotics/tree/master/Path%20Planning)] |
| Multi-image Panorama Stitching | Used OpenCV to implement SIFT, RANSAC and other algorithms to stitch multiple images into a panorama | ![Panorama](assets/images/Panorama/result.jpg "Panorama of a scene from individual images ")  | [[code](https://github.com/salildabholkar/Vision/tree/master/Panorama)] [[demo](https://github.com/salildabholkar/Vision/tree/master/Panorama#other-examples--results)] |
| Game of Life using Deep Neural Net | Created a neural net to simulate [Conway's Game of Life](https://en.wikipedia.org/wiki/Conway%27s_Game_of_Life). Learns to generate the next state from any given random initial state | ![Game of Life](assets/images/GoL/life.gif "Game of Life in action")  | [[code](https://github.com/salildabholkar/Deep-Learning/tree/master/GameOfLife)] |
| SarcDetect| Uses transfer learning for sarcasm detection in English Tweets (via [ULMFiT]({% post_url 2018-06-10-universal-language-model-fine-tuning %})) |  ![Example prediction](https://salildabholkar.github.io/assets/images/sarcasm/predict.png)  | [[blog]({% post_url 2018-09-15-ulmfit-sarcasm-detection %})] |
|--------------+------------+-----------------+----------------|


# Publications
<!-- ACM DL Article: Automatic Document Summarization using Sentiment Analysis -->
<div class="acmdlitem" id="item2980362" style="margin-bottom: 15px"><a href="https://dl.acm.org/authorize?N27517" title="Automatic Document Summarization using Sentiment Analysis">Automatic Document Summarization using Sentiment Analysis</a><div><a href="http://dl.acm.org/author_page.cfm?id=99659084760" >Salil Dabholkar</a>, <a href="http://dl.acm.org/author_page.cfm?id=99659083162" >Yuvraj Patadia</a>, <a href="http://dl.acm.org/author_page.cfm?id=99659083680" >Prajyoti Dsilva</a><br />Proceedings of the International Conference on Informatics and Analytics (ICIA-16). ACM, New York, NY, USA.</div></div>

My first research effort focused on developing a novel mechanism for automatically creating summaries of textual documents.
I found a way to use sentiment analysis along with appropriate fallback mechanisms to achieve the needed results.


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
