---
title: Effective unified index structure for multi-query on massive graph data (under distributed system)
layout: post
tags: 
img: BFSBC.png
categories: ''
---
## Background

因为图形具有对复杂结构建模的高表达能力，将数据建模为图形的应用需求越来越多,并且来自各种学科(如生物网络、社会网络、本体、XML和RDF数据库等)的数据规模爆炸式的增长的图的快速积累激起了广泛的大图查询的需求。处理大规模图数据的能力对于越来越多的应用程序是至关重要的。面对这样广泛的大图查询的需求，就需要在图上提前建立有效的索引结构以加速查询，提高大图查询的效率。这样广泛的大图查询的需求就要求新的建立在图数据上的索引结构，索引结构不仅要使用户能够高效地访问查询图数据，而且也要有效的减小图数据库的系统空间占用，但是若采用分别为每一种查询建立独立的索引结构这样的方法将占用大量的系统空间，导致图数据库的性能急剧下降，不能被真正的应用。因此，本文提出了一种新的多查询统一索引结构以及该索引结构的构建算法，可以同时满足图上的可达、最短路径、图匹配三种查询，采用本文的索引结构就可以避免分别对这三种查询建立三个索引所引起的内存空间的浪费以及性能的下降。

Because of the high expression ability of complex graph structure modeling, the application demand of data modeling as graphics is increasing, and the rapid accumulation of data from various disciplines (such as biological network, social network, ontology, XML and RDF database, etc.) has aroused the demand of extensive large-scale graph-based query. The ability to process large-scale graph data is critical for more and more applications. In the face of such a wide range of large-scale query requirements, it is necessary to establish an effective index structure on the graph in advance to speed up the query and improve the efficiency of large-scale query. Such a wide range of large-scale query needs a new index structure based on graph data. **The index structure should not only enable users to access the query graph data efficiently, but also effectively reduce the system space occupation of graph database. However, if the independent index structure is established for each query, this method will occupy a lot of system space, resulting in the performance of the database to decline sharply, so it can't be used in real application.** Therefore, this paper **proposes a new multi query unified index structure and the construction algorithm of the index structure, which can meet the three queries of reachability, shortest path and graph matching at the same time**. By using the index structure of this paper, we can **avoid the waste of memory space and performance degradation caused by the establishment of three indexes for these three queries respectively**.


The specific process can be described in the following figure:

<center>
<img src="{{site.baseurl}}/assets/img/DBQAflow.png" width="55%" height="55%" /><br>
<div style="color:orange; border-bottom: 1px solid #d9d9d9;
    display: inline-block;
    color: #999;
    padding: 2px;">project process</div><br>
</center>
## Contributions


1. 设计了一个可以同时满足图上的可达、最短路径、图匹配三种查询的统一的索引结构。
2. 提出了一个在时间和空间具有高效性的基于2-hop点的统一索引的构建算法。
3. 在统一索引构建算法中打破了传统的2-hop点的选取方案，采用了基于剪切的BFS搜索算法，能够选取到正确的且具有好的空间性能的hop cover。该算法可以在运行时动态剪切，有效的缩减图的规模。
4. 提出了通过将要匹配的模式图分解单条边的形式后，再将每边的匹配结果进行join，从而便捷高效的借助索引，快速得到图匹配的结果的图匹配查询方法。


1. A unified index structure is designed which can satisfy the reachability, shortest path and graph matching.
2. An efficient 2-hop point based construction algorithm for the unified index is proposed.
3. In the unified index building algorithm, the traditional 2-hop point selection scheme is broken, and the BFSBC algorithm (BFS  Based on Clipping) is adopted, which can select the correct hop cover with good spatial performance. The algorithm can cut dynamically at run time and reduce the size of graph effectively.
4. A graph matching query method is proposed, which decomposes the pattern graph to be matched into single edges, and then joins the matching results of each edge, so as to obtain the graph matching results quickly with the help of index.

## Pseudocode

**Program 1 ：BFSBC ($G$，$v_k$， $L_{k-1}^{'}$)**
1   Q ← A queue with only one element $v_k$
2   for all $v∈V(G) - {v_k}，P [v_k] ← 0 $ and $P [v] ← +∞$
3   for all $v∈V(G)，L_k^{'} [v] ← L_{k-1}^{'} [v]$
4   when $Q$ is not empty:
5   	pop-up head element $u$ in $Q$
6		If $Query(v_k,u,L_{k-1}^{'}) <= P[u]$ then
7			continue
8		$L_k^{'} [u]←L_{k-1}^{'} [u]∪ \{(v_k,P[u])\}$
9		mark $v_k$ as hop point
10		for all $w ∈ N_G (v)$  where $P[w] = +∞$
11			$P[w] = P[u] + 1$
12			put $w$ into $Q$
13	return $L_k^{'}$

**Program 2 ：Calculating 2-hop Coverage by BFSBC Algorithm (G)**
1   for all $v ∈ V(G),L_0^{'} [v]= ϕ$
2   for $k ←1 $ to $ n$
3   	$L_k^{'} $ $←$ BFSBC ($G，v_k， L_{k-1}^{'}$)
4   return $L_n^{'}$

最终通过程序2，对于给定的点的遍历顺序，调用程序1中的剪切BFS算法每次更新上一次所得的索引结构，得到的返回结果就是初步计算出在大图上的全局性的索引结构，同时在索引中出现的点所构成的集合即为2-hop覆盖。
Finally, through program 2, for a given traversal order of points, call the BFSBC algorithm in program 1 to update the index structure each time. **The result is that the initially global index structure on the graph, and the set of points appearing in the index is 2-hop coverage.**

要证明选择了正确的2-hop cover，只需要证明对于任意的0 ≤k≤n, 以及对任意的顶点对v,t 满足 QUERY(s,t,L_k^') = QUERY(s,t,L_k)，这里符号为剪切BFS方法建立的索引L_k^'，通过其他方法建立的正确2-hop cover的索引为L_k。

To prove that the correct 2-hop cover is selected, we just need to prove that $QUERY (s, t, L_k^{'}) = QUERY (s, t, L_K)$ is satisfied for any $0 < K < n$, and for any pair of vertices $v, t$, where $L_k^{'}$ is the index created by BFSBC and $L_K$ is  the index  created by other correct 2-hop cover computing methods. The details demonstrating process can be found in my paper from 

From the demonstrating process, we can show that BFSBC can select the correct 2-hop cover and can accurately answer the relative distance queries.

**Program 3：Hop point index update algorithm $(G， L_k)$**
1   when there is a hop point $v_h$ in $G$ that has not been traversed as a starting point
2   	for all $v ∈ V(G)$，query whether $v$ can reach $v_h$ by index $L_k$
3   		if $v$ can reach $v_h$ then
4				determine the type of point $v$, get type $A$, add ($A, v$) to the reachLable field of $L_K[v_h]$
5			else
6				continue
7	return updated $L_k$

**Program 4 ：$W$ table building algorithm $(G， L_k)$**
1   for $A,B∈T$，$T$ is a collection of all types of points in $G$, creating corresponding table entries for the $W$ table in the form of binaries $(A, B)$
2   for each hop point $v_h ∈ G$，examine each table item $ (A, B)$ in table $W$
3   		if $L_k [v_h]$.reachLabel.contains($A$)&& $L_k [v_h]$.reachLabel.contains($B$) then
4				$W(A,B) ← v_h$
5			else
6				continue
7	return $W$表
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
<img src="{{site.baseurl}}/assets/img/pattern graph.png" width="55%" height="55%" /><br>
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
可以看到在测试图上图索引生成的时间为242477毫秒(ms)=4.0412833(min)。由于hop点是实际作为索引的点，所以可以看到该索引构建算法具有良好的空间性能。
We can see that on the test chart, the index generation time is 24242477 milliseconds = 4.0412833 (min). The set size of Hop cover is 25% of the actual number of vertices. Since hop points are the actual points to be indexed, you can see that the index building algorithm has good spatial performance.
<center>
<img src="{{site.baseurl}}/assets/img/match graph.JPG" width="55%" height="55%" /><br>
<div style="color:orange; border-bottom: 1px solid #d9d9d9;
    display: inline-block;
    color: #999;
    padding: 2px;">Graph matching query</div><br>
</center>
We can see that accessibility query time on the index built on the test chart is 55.418 seconds.