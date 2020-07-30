---
title: One-stop Artificial Intelligence Class Assistant App
layout: post
tags: 
img: class.jpg
---

In this work, we develop an application that is aimed at the 2020 National University IoT Design Competition.  My team members : **Weihong Zhong, Wenjie Ten, Jianyu Xiong**.

## Project Value

本项目面向线下课堂中，同学们在课后对课堂内容有高效复习需求的场景。致力于填补当前线下教育辅助工具对于课程内容的归纳、总结及精炼的空白。

This project is aimed at the **scene where students need to review the classroom content efficiently after class**. We are committed to filling in the gaps in the induction, summary and  refinement of curriculum content in current educational auxiliary tools. 

我们通过使用智能终端对课堂的多种来源数据，包括课程录音、课件、板书等学生拍摄的照片和即时反馈与讨论等内容进行深度的抽取和组织，以将课件为载体，各种资源链接到课件页面的形式提供给学生对课堂内容的快速回顾，以进一步提高学生的复习效率。

We use intelligent terminals to **extract and organize in-depth the data from various sources in the classroom**, including the photos taken by students, course recording, courseware, blackboard writing, and instant feedback and discussion, so as to **provide students with a quick review of the classroom content in the form of courseware as the carrier and various resources linked to the courseware page, to further improve the review efficiency of students**.

我们使用智能终端进行数据采集，能够方便快捷地进行课程录音与课件、录音的上传，尽可能减少其对原教学方案的影响。同一堂课的学生也能够对课堂内容进行拍照记录和上传。

By using the intelligent terminal, we can conveniently and quickly upload the course recording, courseware and recording, and **reduce the impact on the original teaching scheme as much as possible**. Students in the same class can also take photos and upload the content.

我们基于智能终端开发了便捷的重难点标记按钮，学生可以方便快捷地进行重难点标记，物联网云平台后端会即时统计、记录同学们的标记，将照片上传得到的课堂内容进行存储，并将内容与课件的对应页面进行关联，提高了课堂效率和复习效率。

Besides, we have developed a **convenient key and difficult mark button**, which enables students to mark the key and difficult points conveniently and quickly. **The back end of the Internet cloud platform** will immediately count and record the marks of students, store the classroom content uploaded by photos, and associate the content with the corresponding page of the lesson, so as to improve the classroom efficiency and review efficiency.

通过使用我们的app，学生在课后即能够使用智能终端进行课程的全面回顾。学生能查看以课件为载体的课堂回顾，在课件的每一个页面，都展示了该页对应的录音，板书，以及对应页的讨论。学生能够查看重难点标记的统计信息、为课堂内容生成的关键词图等。

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


我们首先对收集到的课程录音进行基于深度全序列卷积神经网络（DFCNN，Deep Fully Convolutional Neural Network）识别框架的语音转写

Firstly, we transcribe the collected course recordings to text based on the **deep full sequence convolutional neural network (DFCNN) recognition framework**.

我们从转写出的文本中使用TextRank技术提取出关键词，针对关键词数量不足的问题，我们将 Wiki 提供的 Xml 格式语料 利用维基百科处理类WikiCorpus 处理成纯文本，进行 Word2vec 的训练，得到了一个基于维基百科语料的 Word2vec 模型，使用基于词向量的近义词抽取技术，拓展文章中的关键词，并依据语义提出类似N-gram 语法模型的方法建立关键词之间的关系。

We use the TextRank technology to extract keywords from the converted text. To solve the problem of insufficient keywords, we **process the XML format corpus provided by WiKi into pure text** by using Wikipedia processing class WiKiCorpus, and then train to **get a word2vec model based on Wikipedia corpus**. In the model, **the synonym extraction technology** based on word vector is used to expand the keywords in the article, and **a method similar to n-gram grammar model is proposed to establish the relationship between keywords**.

我们根据语音转写中的句子与数字语音信号相应的音频段对齐信息，建立结构化的知识元素到原语音信号元素(音频句子等)的映射。且使用数据库记录PPT翻页动作、学生重难点标记、音频、文本四者之间的对应关系。

According to the alignment information between the sentences in speech transcription and the corresponding audio segments of digital speech signals, we establish **the mapping of structured knowledge elements to the original voice signal elements (audio sentences, etc.)**. The corresponding relationship among time of teacher' s PowerPoint page turning action, students' marks of key and difficult points, audio and text **is recorded in our database**.

我们在 Visual  Studio 平台使用 VSTO 开发 PowerPoint 插件，这部分的开发需要使用 C#。我们主要设计了登陆功能，可以在 PowerPoint 端输入用户信息，向后台发送，登陆成功后可以选择课程开始上课；还设计了上传文件模块，通过使用HttpWebRequest 进行多客户端时间同步，向远程服务器上传课件、 音频、 时间轴等文件； 还有时间轴记录模块，通过使用 VSTO 内置的接口获取课件的翻页时间， 以时间轴的形式发送到服务器用以对齐音频和课件。

**We use VSTO to to develop PowerPoint plug-ins in the Visual Studio platform. The development of this part needs to use C#**. We mainly designed the **login function**, which can input user information in PowerPoint terminal and send it to the background. After successful  login, we can choose the course to start class. We also designed the  **upload file module, which uses Httpwebrequest for multi client time synchronization** to upload courseware, audio, time axis and other files  to the remote server. There is also a **timeline recording module**, which  uses the built-in interface of VSTO obtains the page turning time of  courseware and sends it to the server in the form of time axis to align  audio and courseware. 

我们首先使用 Microsoft  recognizers_date_time 识别文本句中是否含有日期，然后通过syntactic parsing分析语句的依存句法关系，按照含有日程信息的大数据归纳出来句法规则对含有日期的文本进行判断，实现日程的抽取。

As for the schedule extracting model, we started with **recognizers_date_time of Microsoft** to identify whether a text sentence contains a date, and then analyzes the **dependency syntactic relationship of the sentence by syntactic parsing**. According to the big data containing the schedule information, the **syntax rules are summarized to judge whether the text containing date is to arrange schedule**, so as to realize the schedule extraction.

## Project Presentation
The following pictures are some screenshot from our appliction to present several functional interface.
<center>
<img src="{{site.baseurl}}/assets/img/User login module.png " width="10%" height="10%" /><br>
<div style="color:orange; border-bottom: 1px solid #d9d9d9;
    display: inline-block;
    color: #999;
    padding: 2px;">User login module</div>
</center>

<center>
<img src="{{site.baseurl}}/assets/img/Recording transcription and keyword extraction module.png "  /><br>
<div style="color:orange; border-bottom: 1px solid #d9d9d9;
    display: inline-block;
    color: #999;
    padding: 2px;">Recording transcription and keyword extraction module</div>
</center>

<center>
<img src="{{site.baseurl}}/assets/img/Course details interface.png "  /><br>
<div style="color:orange; border-bottom: 1px solid #d9d9d9;
    display: inline-block;
    color: #999;
    padding: 2px;">Course details interface</div>
</center>

<center>
<img src="{{site.baseurl}}/assets/img/Course query interface.png "  /><br>
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