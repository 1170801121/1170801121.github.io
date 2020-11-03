---
title: One-stop Intelligent Class Assistant App
layout: post
tags: 
img: class.jpg
---

In this work, we develop an application to help students review more effectively.  My team members : **Weihong Zhong, Wenjie Ten, Jianyu Xiong**. We have already put the app to use in our university’s seminars and received over 200 positive comments from students and teachers!

## Project Value


This project is aimed at the **scene where students need to review the classroom content efficiently after class**. We are committed to filling in the gaps in the induction, summary and  refinement of curriculum content in current educational auxiliary tools. 


We use intelligent terminals to **extract and organize in-depth the data from various sources in the classroom**, including the photos taken by students, course recording, courseware, blackboard writing, and instant feedback and discussion, so as to **provide students with a quick review of the classroom content in the form of courseware as the carrier and various resources linked to the courseware page, to further improve the review efficiency of students**.


By using the intelligent terminal, we can conveniently and quickly upload the course recording, courseware and recording, and **reduce the impact on the original teaching scheme as much as possible**. Students in the same class can also take photos and upload the content.


Besides, we have developed a **convenient key and difficult mark button**, which enables students to mark the key and difficult points conveniently and quickly. **The back end of the Internet cloud platform** will immediately count and record the marks of students, store the classroom content uploaded by photos, and associate the content with the corresponding page of the lesson, so as to improve the classroom efficiency and review efficiency.


Through the use of our project, students can use the intelligent terminal to **conduct a comprehensive review of the course after class**. Students can **view the classroom review with courseware as the carrier**. On each page of the courseware, the corresponding recording, blackboard writing and discussion of the corresponding page are displayed. Students can **view the statistical information** of the key and difficult points, the keyword map generated for the class content, etc.

The **processing logic flow chart** of our project is as follows.
<center>
<img src="{{site.baseurl}}/assets/img/logic_1.png "  /><br>
<div style="color:orange; border-bottom: 1px solid #d9d9d9;
    display: inline-block;
    color: #999;
    padding: 2px;">processing logic flow chart</div>
</center>

The **overall architecture design drawing** of our project is as follows.
<center>
<img src="{{site.baseurl}}/assets/img/logic_2.png "  /><br>
<div style="color:orange; border-bottom: 1px solid #d9d9d9;
    display: inline-block;
    color: #999;
    padding: 2px;">overall architecture design drawing</div>
</center>
## Technical Overview


Firstly, we transcribe the collected course recordings to text based on the **deep full sequence convolutional neural network (DFCNN) recognition framework**.


We use the TextRank technology to extract keywords from the converted text. To solve the problem of insufficient keywords, we **process the XML format corpus provided by WiKi into pure text** by using Wikipedia processing class WiKiCorpus, and then train to **get a word2vec model based on Wikipedia corpus**. In the model, **the synonym extraction technology** based on word vector is used to expand the keywords in the article, and **a method similar to n-gram grammar model is proposed to establish the relationship between keywords**.


According to the alignment information between the sentences in speech transcription and the corresponding audio segments of digital speech signals, we establish **the mapping of structured knowledge elements to the original voice signal elements (audio sentences, etc.)**. The corresponding relationship among time of teacher' s PowerPoint page turning action, students' marks of key and difficult points, audio and text **is recorded in our database**.


**We use VSTO to to develop PowerPoint plug-ins in the Visual Studio platform. The development of this part needs to use C#**. We mainly designed the **login function**, which can input user information in PowerPoint terminal and send it to the background. After successful  login, we can choose the course to start class. We also designed the  **upload file module, which uses Httpwebrequest for multi client time synchronization** to upload courseware, audio, time axis and other files  to the remote server. There is also a **timeline recording module**, which  uses the built-in interface of VSTO obtains the page turning time of  courseware and sends it to the server in the form of time axis to align  audio and courseware. 


As for the schedule extracting model, we started with **recognizers_date_time of Microsoft** to identify whether a text sentence contains a date, and then analyzes the **dependency syntactic relationship of the sentence by syntactic parsing**. According to the big data containing the schedule information, the **syntax rules are summarized to judge whether the text containing date is to arrange schedule**, so as to realize the schedule extraction.

## Project Presentation
The following pictures are some screenshot from our appliction to present several functional interface.
<center>
<img src="{{site.baseurl}}/assets/img/User login module.JPG " /><br>
<div style="color:orange; border-bottom: 1px solid #d9d9d9;
    display: inline-block;
    color: #999;
    padding: 2px;">User login module</div>
</center>

<center>
<img src="{{site.baseurl}}/assets/img/Recording transcription and keyword extraction module.JPG "  /><br>
<div style="color:orange; border-bottom: 1px solid #d9d9d9;
    display: inline-block;
    color: #999;
    padding: 2px;">Recording transcription and keyword extraction module</div>
</center>

<center>
<img src="{{site.baseurl}}/assets/img/Course details interface.JPG "  /><br>
<div style="color:orange; border-bottom: 1px solid #d9d9d9;
    display: inline-block;
    color: #999;
    padding: 2px;">Course details interface</div>
</center>

<center>
<img src="{{site.baseurl}}/assets/img/Course query interface.JPG "  /><br>
<div style="color:orange; border-bottom: 1px solid #d9d9d9;
    display: inline-block;
    color: #999;
    padding: 2px;">Course query interface</div>
</center>

<center>
<img src="{{site.baseurl}}/assets/img/Recording function module.JPG "  /><br>
<div style="color:orange; border-bottom: 1px solid #d9d9d9;
    display: inline-block;
    color: #999;
    padding: 2px;">Recording function module</div>
</center>

<center>
<img src="{{site.baseurl}}/assets/img/Teacher intelligent terminal control interface.png "  /><br>
<div style="color:orange; border-bottom: 1px solid #d9d9d9;
    display: inline-block;
    color: #999;
    padding: 2px;">Teacher intelligent terminal control interface</div>
</center>

<center>
<img src="{{site.baseurl}}/assets/img/Login interface of teacher terminal.png "  /><br>
<div style="color:orange; border-bottom: 1px solid #d9d9d9;
    display: inline-block;
    color: #999;
    padding: 2px;">Login interface of teacher terminal</div>
</center>