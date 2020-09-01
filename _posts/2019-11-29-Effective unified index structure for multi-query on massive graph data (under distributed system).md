---
title: Effective unified index structure for multi-query on massive graph data (under distributed system)
layout: post
tags: 
img: BFSBC.png
categories: ''
---
## Background

Because of the high expression ability of complex graph structure modeling, the application demand of data modeling as graphics is increasing, and the rapid accumulation of data from various disciplines (such as biological network, social network, ontology, XML and RDF database, etc.) has aroused the demand of extensive large-scale graph-based query. The ability to process large-scale graph data is critical for more and more applications. In the face of such a wide range of large-scale query requirements, it is necessary to establish an effective index structure on the graph in advance to speed up the query and improve the efficiency of large-scale query. Such a wide range of large-scale query needs a new index structure based on graph data. **The index structure should not only enable users to access the query graph data efficiently, but also effectively reduce the system space occupation of graph database. However, if the independent index structure is established for each query, this method will occupy a lot of system space, resulting in the performance of the database to decline sharply, so it can't be used in real application.** Therefore, this paper **proposes a new multi query unified index structure and the construction algorithm of the index structure, which can meet the three queries of reachability, shortest path and graph matching at the same time**. By using the index structure of this paper, we can **avoid the waste of memory space and performance degradation caused by the establishment of three indexes for these three queries respectively**.

## Contributions


1. A unified index structure is designed which can satisfy the reachability, shortest path and graph matching.
2. An efficient 2-hop point based construction algorithm for the unified index is proposed.
3. In the unified index building algorithm, the traditional 2-hop point selection scheme is broken, and the BFSBC algorithm (BFS  Based on Clipping) is adopted, which can select the correct hop cover with good spatial performance. The algorithm can cut dynamically at run time and reduce the size of graph effectively.
4. A graph matching query method is proposed, which decomposes the pattern graph to be matched into single edges, and then joins the matching results of each edge, so as to obtain the graph matching results quickly with the help of index.

## Pseudocode

**Program 1 ：BFSBC ($G$，$v_k$， $L_{k-1}^{'}$)**
<center>
<img src="{{site.baseurl}}/assets/img/BFSBC.JPG" width="55%" height="55%" /><br>
</center>


**Program 2 ：Calculating 2-hop Coverage by BFSBC Algorithm (G)**
<center>
<img src="{{site.baseurl}}/assets/img/p2.JPG" width="25%" height="25%" /><br>
</center>

Finally, through program 2, for a given traversal order of points, call the BFSBC algorithm in program 1 to update the index structure each time. **The result is that the initially global index structure on the graph, and the set of points appearing in the index is 2-hop coverage.**


To prove that the correct 2-hop cover is selected, we just need to prove that $QUERY (s, t, L_k^{'}) = QUERY (s, t, L_K)$ is satisfied for any $0 < K < n$, and for any pair of vertices $v, t$, where $L_k^{'}$ is the index created by BFSBC and $L_K$ is  the index  created by other correct 2-hop cover computing methods. The details demonstrating process can be found in my paper from 

From the demonstrating process, we can show that BFSBC can select the correct 2-hop cover and can accurately answer the relative distance queries.

**Program 3：Hop point index update algorithm $(G， L_k)$**
<center>
<img src="{{site.baseurl}}/assets/img/p3.JPG" width="55%" height="55%" /><br>
</center>

**Program 4 ：$W$ table building algorithm $(G， L_k)$**
<center>
<img src="{{site.baseurl}}/assets/img/p4.JPG" width="55%" height="55%" /><br>
</center>

**Program 3 and program 4 are used to establish and update the index using global index from program 1 and 2.** More details can be found in my paper.


## Query example
<center>
<img src="{{site.baseurl}}/assets/img/BFSBC.png" width="55%" height="55%" /><br>
<div style="color:orange; border-bottom: 1px solid #d9d9d9;
    display: inline-block;
    color: #999;
    padding: 2px;">An example shows the process of BFSBC search</div><br>
</center>

The following illustration illustrates the query process for graph matching:
<center>
<img src="{{site.baseurl}}/assets/img/example graph.png" width="55%" height="55%" /><br>
<div style="color:orange; border-bottom: 1px solid #d9d9d9;
    display: inline-block;
    color: #999;
    padding: 2px;">Example graph</div><br>
</center>

<center>
<img src="{{site.baseurl}}/assets/img/pattern graph.png" width="20%" height="20%" /><br>
<div style="color:orange; border-bottom: 1px solid #d9d9d9;
    display: inline-block;
    color: #999;
    padding: 2px;">Pattern graph</div><br>
</center>

In the example diagram, the pattern diagram shown above is used for pattern matching, and the W table we have created is shown below.
<center>
<img src="{{site.baseurl}}/assets/img/Wtable.png" width="55%" height="55%" /><br>
<div style="color:orange; border-bottom: 1px solid #d9d9d9;
    display: inline-block;
    color: #999;
    padding: 2px;">W table</div><br>
</center>
## Example

The implementation uses the **Spark's Graphx framework for large-scale map processing** and **implemented it in the scala language**.

Experiments data comes from:Http://swat.cse.lehigh.edu/projects/lubm/Read. .The dataset provides a file with a.Owl suffix in the form of a knowledge map backed by University relationships.

<center>
<img src="{{site.baseurl}}/assets/img/indexTime.png" width="55%" height="55%" /><br>
<div style="color:orange; border-bottom: 1px solid #d9d9d9;
    display: inline-block;
    color: #999;
    padding: 2px;">Index generation</div><br>
</center>

We can see that on the test chart, the index generation time is 24242477 milliseconds = 4.0412833 (min). The set size of Hop cover is 25% of the actual number of vertices. Since hop points are the actual points to be indexed, you can see that the index building algorithm has good spatial performance.

<center>
<img src="{{site.baseurl}}/assets/img/match graph.JPG" width="55%" height="55%" /><br>
<div style="color:orange; border-bottom: 1px solid #d9d9d9;
    display: inline-block;
    color: #999;
    padding: 2px;">Shortest path query</div><br>
</center>
We can see that shortest path query time on the index built on the test chart is 0.101525 seconds.

<center>
<img src="{{site.baseurl}}/assets/img/reach.JPG" width="55%" height="55%" /><br>
<div style="color:orange; border-bottom: 1px solid #d9d9d9;
    display: inline-block;
    color: #999;
    padding: 2px;">Accessibility query</div><br>
</center>
We can see that accessibility query time on the index built on the test chart is 0.145033 seconds.

<center>
<img src="{{site.baseurl}}/assets/img/match graph.JPG" width="55%" height="55%" /><br>
<div style="color:orange; border-bottom: 1px solid #d9d9d9;
    display: inline-block;
    color: #999;
    padding: 2px;">Graph matching query</div><br>
</center>
We can see that graph matching query time on the index built on the test chart is 55.418 seconds.