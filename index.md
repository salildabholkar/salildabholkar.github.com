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
I am a budding researcher dabbling in Data Science, Information Retrieval and Artificial Intelligence. 

### Publications
My first research effort focused on developing a novel mechanism for automatically creating summaries of textual documents. I found a way to use sentiment analysis along with appropriate fallback mechanisms to achieve the needed results. The paper was presented in ACM's **"INTERNATIONAL CONFERENCE ON INFORMATICS AND ANALYTICS"** and is available for reading on the [Digital Library](http://dl.acm.org).

### Software Development
I developed a software, lovingly called **"Quibble"**, for the [R&D Department of my institute](http://www.sfitengg.org/R_and_D.php). What initially began as a simple automation and marks curation tool is now developing into an advanced data analysis and visualization software. It allows the teacher to map exam questions to specific *Course Outcomes* and enter marks for students (or provide an excel sheet for past years, which was done manually). The software then automagically performs all the required computations and provides the user with the final CO mapping table with an option to save it as a PDF file.  
All the data from students names, their marks to the CO Mapping is stored in a firebase database and can be used for getting useful insights. Which subjects do the students find difficult? Gender-to-marks relationships? Progress over the years? What are the underrepresented Course Outcomes? The project is still under development and having high expectations from it.


## Blog Posts
<ul class="posts">
  {% for post in site.posts %}
    <h3><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></h3>
	{{ post.excerpt }}
  {% endfor %}
</ul>