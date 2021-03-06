---
title: Document Base Question Answering
layout: post
tags: 
img: DBQAflow.png
categories: ''
---
## Background

The context of this task is the question answering task attempts to answer questions posed in natural  language. The answers come from unstructured text fragments. That is to retrieve the document according to the question, and then use the reading comprehension technology to get the answer from the document according to the question. The specific process can be described in the following figure:

<center>
<img src="{{site.baseurl}}/assets/img/DBQAflow.png" width="55%" height="55%" /><br>
<div style="color:orange; border-bottom: 1px solid #d9d9d9;
    display: inline-block;
    color: #999;
    padding: 2px;">project process</div><br>
</center>
## Task

We address the task about how to quickly retrieve the text containing the answer according to the question. This task is similar to the traditional information retrieval, that is, indexing documents. However, unlike the traditional method, we expect that the input is a question, and the retrieved document should be the document that can answer the question, not the document similar to the question. So we need to map a question to a document that can answer the question.


## Method

1. Use Bert according to https://github.com/hanxiao/bert-as-service  to encode problem and document as fixed dimension vectors, which are denoted as $Q$ and $D$ respectively.
2. Train a matrix $W$ such that $D = WQ$. The data uses the question and document pairs in DuReader. Data comes from http://ai.baidu.com/broad/download?dataset=dureader. Extract the Problem-Document pairs and store them in a serialized file object.
3. Use Annoy (Approximate Nearest Neighbors Oh Yeah) to conduct Approximate nearest neighbor search.
## Result
After applying the effecive method to compute the normal, the expected result is shown in the figure below.
<center>
<img src="{{site.baseurl}}/assets/img/DBQAresult.png" width="55%" height="55%" /><br>
<div style="color:orange; border-bottom: 1px solid #d9d9d9;
    display: inline-block;
    color: #999;
    padding: 2px;">effecience analysis</div><br>
</center>
