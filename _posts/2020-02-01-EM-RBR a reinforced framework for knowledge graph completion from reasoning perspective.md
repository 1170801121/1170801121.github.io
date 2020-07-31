---
title: EM-RBR: a reinforced framework for knowledge graph completion
layout: post
tags: 
img: overview.JPG
categories: ''
---
Beginning from the winter vocation, I attend the **Mass Data Research Center in HIT** as a Research Assistant. In this research experience, I propose a general framework, named EM-RBR(embedding and rule-based reasoning), **capable of combining the advantages of reasoning based on rules and the state-of-the-art models of embedding**. EM-RBR aims to **utilize relational background knowledge contained in rules to conduct multi-relation path prediction** rather than superficial vector triangle linkage in embedding models. By this way, the model can explore relation between two entities in deeper context to achieve higher accuracy. In experiments, we demonstrate that **EM-RBR achieves better performance compared with previous models on FB15k and our new dataset FB15k-R**. We make the implementation of EM-RBR available at https://github.com/1173710224/link-prediction-with-rule-based-reasoning. **Now this paper is in review of NeurIPS 2020!**

## Challenge
In the development of the joint framework EM-RBR, we meet two challenges. On the one hand, it is not feasible and tractable to mine rules manually because it is time-consuming and laborious. A suitable method is to extract rules by some rules-mining algorithms such as AMIE. However, **these rules automatically mined sometimes are not completely credible**. Therefore, it is necessary to propose a reasonable way to measure rules to pick proper rules for the given triplets. On the other hand, it is known that traditional reasoning-based methods will give only 0 or 1 to one triplet to indicate accept or refuse for the given knowledge base. This conventional **qualitative analysis lacks the quantitative information as the embedding models**. So the result of our reasoning-based framework need to reflect the probability that one triplet belongs to the knowledge base more accurately.

## Contribution
Three main contributions in EM-RBR are summarized as follows. Firstly, EM-RBR is **flexible and general enough to optimise any type of embedding models**. Secondly, we give rule a sensible measurement. The evaluation strategy referred as rule embedding **not only takes embedding results into consideration but also unifies the magnitude of embedding and rules' credibility**. Thirdly, we propose novel **rating mechanism combined with reasoning process**, which can distinguish a given triplet with other wrong triplets better.

## Overview of methods
EM-RBR combines embedding and rule-based reasoning. Given a new triplet, we apply rules to conduct reasoning. With the help of the structured information of logic rules in the the same semantic space with embedding, a score can be output by EM-RBR to measure the quality of the result. **More details and relative domenstrations about our model can be seen in our paper.**

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
EM-RBR integrated with TransE, TransH and TransR greatly improve the performance of the original methods on all metrics according to the results in Table 1. This implies that our reasoning-enhanced framework can efficiently help the knowledge graph embedding models to perform link prediction more accurately.
<center>
<img src="{{site.baseurl}}/assets/img/expTable1.JPG" width="55%" height="55%" /><br>
</center>
Our rule-enhanced method **significantly reaches some promising absolute performance scores on Hits@1, Hits@3, and Hits@5 metrics**, e.g., in FB15k,  EM-RBR(H)'s improvements of $38.82 - 30.37 = 8.45$ in Hits@1, $61.13 - 55.53 = 5.60$ in Hits@3 and also obtains $68.28 - 64.09 = 4.19$ absolute improvement in Hits@5. These metrics paying attention on front ranks are the most important in real knowledge inference task. The higer Hits@n score indicates the greater possibilities to rank the the correct triplets in the front.

**More impressively in FB15k-R, EM-RBR(E)'s, EM-RBR(H)'s and EM-RBR(R)'s advance in Hits@1 is $65.1 - 14.9 = 50.2$, $75.45 - 18.25 = 57.20$ and $74.30 - 7.65 = 66.65$ respectively.** Thus, EM-RBR can make knowledge graph embedding method capable of being used in the real and large scale knowledge inference tasks.

The figure 4 and figure 5 used in paper are to show the **hyper-parameter analysis**. And Table 2 is a **case study to explore how much EM-RBR can optimize on each triplet on earth**. Both more elaborate description can be found in our paper.
<center>
<img src="{{site.baseurl}}/assets/img/varAna.JPG" width="55%" height="55%" /><br>
</center>
<center>
<img src="{{site.baseurl}}/assets/img/table2Ana.JPG" width="55%" height="55%" /><br>
</center>