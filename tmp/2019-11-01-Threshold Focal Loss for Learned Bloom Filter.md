---
title: Threshold Focal Loss for Learned Bloom Filter
layout: post
categories: ''
tags: ''
img: LBF.png
---
There has been a recent trend in training neural networks to replace traditional data structures, resulting in reduced false positive rates or greater compression. Learned Bloom Filters, which train a neural network as a pre-filter, enhance classical Bloom Filters and provide better compression. However, previous Learned Bloom Filters trained with cross entropy loss do not take advantage of the fact that Learned Bloom Filters are aimed at minimizing a false negative rate for a fixed false positive rate. In this paper, we explore the effect of loss function on this specific task. We propose Unbalanced Focal Loss and Threshold Focal Loss, both novel loss functions that are able to achieve significant compression gains ( __12.19%__ and __16.7%__ ) over previous Learned Bloom Filter.

## Intuition
The intuition behind Learned Bloom Filter is that there are two main differences between Learned Bloom Filter and general classification problem. The first thing is that for LBT, it has all the positive samples trained during the training step, while for general task, new posi-tive samples could occur in test set. Therefore, for LBT, we should try to make the decision boundary closer to the positive samples. The second difference is that the aim for LBT is to minimize the false negative rate with an ex-tremely low false positive rate. However, the general task just minimizes the loss of incorrect prediction. Based on the second difference, we then propose Unbalanced Focal Loss and Threshold Focal Loss. 

## Unbalanced Focal Loss
The formula is as below.
![Unbalanced Focal]({{site.baseurl}}/assets/img/unbalanced.png)
![Picture]({{site.baseurl}}/assets/img/unbalanced_pic.jpg)

## Threshold Focal Loss
The formula is as below.
![Threshold Focal]({{site.baseurl}}/assets/img/threshold.png)
![Picture]({{site.baseurl}}/assets/img/threshold_pic.jpg)

## Result
Unbalanced focal loss could decrease the memory needed by __12.19%__ , and threshold focal loss could decrease it by __16.72%__ , which demonstrate the promising point to design loss function from a view of probability theory.
![Result1]({{site.baseurl}}/assets/img/result_f.png)
![Result2]({{site.baseurl}}/assets/img/result_t.png)