---
title: Document Base Question Answering
layout: post
tags: 
img: DBQAflow.png
categories: ''
---
## Background
问答任务试图回答自然语言形式提出的问题. 答案来自非结构化的文本片段。即根据问题检索文档，然后利用阅读理解技术，根据问题从文档中获取答案。

The context of this task is the question answering task attempts to answer questions posed in natural  language. The answers come from unstructured text fragments. That is to retrieve the document according to the question, and then use the reading comprehension technology to get the answer from the document according to the question. The specific process can be described in the following figure:

<center>
<img src="{{site.baseurl}}/assets/img/DBQAflow.png" width="55%" height="55%" /><br>
<div style="color:orange; border-bottom: 1px solid #d9d9d9;
    display: inline-block;
    color: #999;
    padding: 2px;">project process</div><br>
</center>
## Task
期望得到的结果就是下图所示的，在这里面我们有一个任务，就是如何能够根据问题将包含答案的文本快速的检索出来。这个任务类似于传统的信息检索，即针对文档做索引进行检索，但是与传统方法不同的是，因为我们期望输入是问题，检索到的文档应该是能够回答问题的文档，而不是与问题类似的文档。所以要做一个问题到可回答问题的文档的映射。

We address the task about how to quickly retrieve the text containing the answer according to the question. This task is similar to the traditional information retrieval, that is, indexing documents. However, unlike the traditional method, we expect that the input is a question, and the retrieved document should be the document that can answer the question, not the document similar to the question. So we need to map a question to a document that can answer the question.


## Method
1.使用https://github.com/hanxiao/bert-as-service 编码问题和文档为固定维度的向量，分别为q和d，
2.训练一个矩阵W，使得d=Wq。数据使用DuReader中的问题和文档对。数据使用http://ai.baidu.com/broad/download?dataset=dureader中的DuReader_v2.0_raw.zip 把里面的问题-文档对抽出出来存在某个文件或者序列化对象中
3.使用https://github.com/spotify/annoy进行近似最近邻搜索


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
