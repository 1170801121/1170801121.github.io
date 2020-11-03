---
title: EM-RBR a reinforced framework for knowledge graph completion
layout: post
tags: 
img: overview.JPG
categories: ''
---
Beginning from October 2019, I worked in **HIT Massive Data Computing Research Center** as a research assistant. And from Feb 2020, I led a group to finish a research on knowledge graph completion. Finally I wrote a paper to summarize this work, as the **first author**, and submitted it to **International Conference on Learning Representations (ICLR) 2021**. You can **download my paper (arXiv:2009.08656) from <https://arxiv.org/abs/2009.08656>.** 

## Abstract
Knowledge graph completion aims to predict the new links in given entities among the knowledge graph (KG). Most mainstream embedding methods focus on fact triplets contained in the given KG, however, ignoring the rich background information provided by logic rules driven from knowledge base implicitly. To solve this problem, in this paper, we propose a general framework, named EM-RBR(embedding and rule-based reasoning), **capable of combining the advantages of reasoning based on rules and the state-of-the-art models of embedding**. EM-RBR aims to **utilize relational background knowledge contained in rules to conduct multi-relation reasoning link prediction** rather than superficial vector triangle linkage in embedding models. By this way, we can explore relation between two entities in deeper context to achieve higher accuracy. In experiments, we demonstrate that **EM-RBR achieves better performance compared with previous models on FB15k, WN18 and our new FB15k-R dataset, especially where our model performs further better than those state-of-the-arts** . We make the implementation of EM-RBR available at https://github.com/1173710224/link-prediction-with-rule-based-reasoning.

## Challenge
In the development of the joint framework EM-RBR, we meet two challenges. On the one hand, it is not feasible and tractable to mine rules manually because it is time-consuming and laborious. A suitable method is to extract rules by some rules-mining algorithms such as AMIE. However, **these rules automatically mined sometimes are not completely credible**. Therefore, it is necessary to propose a reasonable way to measure rules to pick proper rules for the given triplets. On the other hand, it is known that traditional reasoning-based methods will give only 0 or 1 to one triplet to indicate acceptance or rejection for the given knowledge graph. This conventional **qualitative analysis lacks the quantitative information as the embedding models**. So the result of our reasoning-based framework need to reflect the probability of one triplet belonging to the knowledge graph.

## Contribution
Three main contributions in EM-RBR are summarized as follows. Firstly, EM-RBR is **flexible and general enough to optimise  a lot of embedding models**. Secondly, we developed **a scalable matrix approach** that puts the structured rule information and embedding results into the same semantic space to evaluate the rules. Thirdly, we propose **a novel rating mechanism to combine with a reasoning process**, which can distinguish a given triplet with other wrong triplets better.

## Overview of methods
EM-RBR combines embedding and rule-based reasoning. Given a new triplet, we apply rules to conduct reasoning. With the help of the structured information of logic rules and embedding in the same semantic space, a score can be output by EM-RBR to measure the probability of one given triplet belonging to the knowledge graph. **More details and relevant demonstrations about our model can be seen in our paper.**

The following picture shows the an overview of our framework.
<center>
<img src="{{site.baseurl}}/assets/img/overview.JPG" width="55%" height="55%" /><br>
<div style="color:orange; border-bottom: 1px solid #d9d9d9;
    display: inline-block;
    color: #999;
    padding: 2px;">An overview of our framework.</div><br>
</center>
The figure 2 and figure 3 used in paper are the simple illustration of measuring a rule and score function.
<center>
<img src="{{site.baseurl}}/assets/img/simpleExp.JPG" width="55%" height="55%" /><br>
</center>
## Experiment

**Baseline**: To demonstrate the effectiveness of EM-RBR, we compare with a number of competitive baselines: TransE (Bordes et al., 2013), TransH (Wang et al., 2014), TransR (Lin et al., 2015), TransD (Ji et al., 2015), RUGE (Guo et al., 2017), ComplEx (Trouillon et al., 2016) and DistMult (Kadlec et al., 2017). All baselines are evaluated on FB15k-R. Besides, TransE, TransH, TransR and TransD are evaluated on FB15k and WN18 to prove that our framework is a real reinforced framework.

Experimental Results are as shown in Table 1. When evaluating on FB15k and WN18, our model has improved all the metrics compared with the translation model in the baselines, especially MRR and Hits@1 on WN18. The higer Hits@n score indicates the greater possibilities to rank the the correct triplets in the front. These metrics paying attention on front ranks are the most important in real knowledge inference task. For example, **EM-RBR(D) improve Hits@1 on WN18 from 0.296 to 0.752 compared to TransD**.

As for FB15k-R, each triplet in this data set can match enough rules so that they can be optimized under EM-RBR. On this data set, the best MR is **1.73** from EM-RBR(R) which is an improvement of **24.93** relative to RotateE. The best MRR is **0.86** from EM-RBR(R) which is an improvement of **0.35** relative to ComplEx. The best Hits@1 is **0.7545** from EM-RBR(H) which is an improvement of **39.65** relative to ComplEx. The best Hits@10 is **0.992** from EM-RBR(R) which is an improvement of **20.2** relative to ComplEx.

<center>
<img src="{{site.baseurl}}/assets/img/expTable1.JPG" width="55%" height="55%" /><br>
</center>

The figure 4 and figure 5 used in paper are to show the **hyper-parameter analysis**. And Table 2 is an **optimized case analysis**.
<center>
<img src="{{site.baseurl}}/assets/img/varAna.JPG" width="55%" height="55%" /><br>
</center>
<center>
<img src="{{site.baseurl}}/assets/img/table2Ana.JPG" width="55%" height="55%" /><br>
</center>