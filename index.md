---
layout: page
title: Salil Dabholkar
tagline: Welcome to Salil's Mind Palace!
description: Salil Dabholkar takes you on a tour of his Mind Palace. Know more about him and his interests. Salil is an aspiring Web Developer and Programmer and is currently a student in St. Francis Institute of Technology.
keywords: Salil, Salil Dabholkar, Salil Blog, UltimateSupreme, SFIT, St. Francis Institute of Technology, Research
---
{% include JB/setup %}

## About me
My name is Salil. On the internet I am known by the nicknames "UltimateSupreme" (since long ago, too long to get rid of) or "UltiSup" (much more unique). Currently a student studying "Information Technology" in [St. Francis Institute of Technology](http://www.sfitengg.org), I am an aspiring Web Developer and Programmer.

My primary skill is solid knowledge of end-to-end web development using CSS, HTML, JavaScript and bit of PHP.
I am also good with few general purpose programming languages like C, Java and Ruby. Though these are the weapons of my choice, I do not favour one language over the other. Each language has its own elegance and style of winning you the war. Like any good programmer worth his salt, I can learn a new one easily enough if I have a reason to.  
Recently, I have been meddling with and taken a keen interest towards Data Science and Artificial Intelligence especially after my course work in "Data Mining and Business Intelligence" and "Intelligent Systems".

I have very good hygiene and outstanding hair :)
I occasionally like to bake a cake.


## Research Experience
I am a budding researcher dabbling in Data Science, Information Retrieval and Artificial Intelligence.

### Publications
<!-- ACM DL Article: Automatic Document Summarization using Sentiment Analysis -->
<div class="acmdlitem" id="item2980362"><img src="https://dl.acm.org/images/oa.gif" width="25" height="25" border="0" alt="ACM DL Author-ize service" style="vertical-align:middle"/><a href="https://dl.acm.org/authorize?N27517" title="Automatic Document Summarization using Sentiment Analysis">Automatic Document Summarization using Sentiment Analysis</a><div style="margin-left:25px"><a href="http://dl.acm.org/author_page.cfm?id=99659084760" >Salil Dabholkar</a>, <a href="http://dl.acm.org/author_page.cfm?id=99659083162" >Yuvraj Patadia</a>, <a href="http://dl.acm.org/author_page.cfm?id=99659083680" >Prajyoti Dsilva</a><br />ICIA-16 Proceedings of the International Conference on Informatics and Analytics, 2016</div></div>
<!-- ACM DL Bibliometrics: Automatic Document Summarization using Sentiment Analysis-->
<div class="acmdlstat" id ="stats2980362"><iframe src="https://dl.acm.org/authorizestats?N27517" width="100%" height="30" scrolling="no" frameborder="0">frames are not supported</iframe></div>

My first research effort focused on developing a novel mechanism for automatically creating summaries of textual documents. I found a way to use sentiment analysis along with appropriate fallback mechanisms to achieve the needed results. The paper was presented in ACM's **"INTERNATIONAL CONFERENCE ON INFORMATICS AND ANALYTICS"** and is available for reading in the [Digital Library](http://dl.acm.org).

### R&D Software
I developed a software, lovingly called **"Quibble"**, for the [R&D Department of my institute](http://www.sfitengg.org/R_and_D.php). What initially began as a simple automation and marks curation tool is now developing into an advanced data analysis and visualization software. It allows the teacher to map exam questions to specific *Course Outcomes* and enter marks for students (or provide an excel sheet for past years, which was done manually). The software then automagically performs all the required computations and provides the user with the final CO mapping table with an option to save it as a PDF file. [Read more..]({% post_url 2016-08-20-quibble %})  
All the data from students names, their marks to the CO Mapping is stored in a firebase database and can be used for getting useful insights. Which subjects do the students find difficult? Gender-to-marks relationships? Progress over the years? What are the underrepresented Course Outcomes? The project is still under development and having high expectations from it.

### Final Year Project
My final year project aims to eradicate the hassle and frustrations of having to remember various syntax and repeatedly type in code for creation of similar programs. All languages include the same basic elements but what makes them difficult to understand is the incredible variety of odd syntax that people use to say the same basic things. Some use terse notation involving odd punctuation (APL being an extreme). Some use lots of keywords (COBOL being an excellent representative). An excellent way of overcoming such a problem is by creating an **abstraction** over such diversities. Often overlooked way of achieving this feat is the decreasing the use of text and increasing the amount of work done by Visual Drag and Drop tools.  
The aim of this project is to abstract away the complexities involved in textual programming languages by creating a visual interface consisting of several graphical tools which provide a user-friendly programming experience for beginners. The graphical tools will enable the user to develop programs visually without the need to worry about different syntax and semantics of different programming languages. The software will then have an option of automatically generating code in the specified programming language. Thus, the user can use the existing compilers or interpreters to execute their programs (JVM, Visual C, etc). The users thus also maintain the ability to further optimize their code by hand, generating only prototypes of their codes by the Graphical tool.


## Blog Posts
<div class="posts">
  {% for post in site.posts %}
    <h3><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></h3>
	{{ post.excerpt }}
  {% endfor %}
</div>
