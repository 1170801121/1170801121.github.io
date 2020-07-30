---
layout: post
title: Intelligent Robot System for Quoridor
date: Oct.2017-Jun.2018
description: This is one project in hit smart club.
fig-caption: 'null'
tags: HIT
categories: ''
img: quoridor.JPG
---
Luckily, I was selected as a member of HIT Smart Car Innovational Club in Oct.2017 , a club that is aimed at the 13th National University NXP Cup of Smart Car Competition. And our first task was that a 8x8 blue checkboard marked with numbers lied 8 white chess pieces randomly, and the robot should make the 8 pieces meet the eight queens principle in the checkboard. Besides, our final task is that we should design a robot that can play Quoridor against others in the checkboard. My team members:__Chengzhe Han, Yuhang Ge, Xianyang Qi, Chenxing Cai__.

![Our team]({{site.baseurl}}/assets/img/we_quoridor.JPG)
## Working on viusal SLAM
In the team, I was fully responsible for __image processing__. I learned to use library functions in Opencv to undistort source image, develop code for inversing perspective transformation. However, for image segmentation, I confronted a problem that thresholding processing didn’t work under the uneven light. To solve this problem, I referred to the Internet for help and finally found the Canny edge detection theory to segment the squares in the image and it really worked well even under poor lighting conditions. Then the next difficulty is that how it can identify the number on each square. This time I apply the neural network for numerical recognition. I spent one whole week collecting images, extracting digits, digital sorting and training a back propagation neural network in the end and the success ratio of numerical recognition was __98.3%__.

![Program]({{site.baseurl}}/assets/img/smart_car_pro.png)

## Our Achievement
Still, the next challenge was that some numbers were covered by the chess pieces so they couldn’t be identified. After thinking for a few days, I came up with a method that digital correction could be added after digital recognition. Since the relative location in the image between two numbers means the relative value. If they meet a certain rule, then the two numbers’ correct time plus one. And I’ll select the number whose correct time is largest as the mother number to correct other numbers. After identifying all the numbers correctly, we could calculate the robot’s location and direction in the real world at last. With our team’s hard work, we won the __fourth place__ in the 13th National University NXP Cup of Smart Car Competition at last.

![Our team]({{site.baseurl}}/assets/img/comp1.JPG)

<iframe width="560" height="315" src="https://www.youtube.com/embed/2lKA9qoncAA" frameborder="0" allowfullscreen></iframe>