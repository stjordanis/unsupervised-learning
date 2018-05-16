# [Network Analysis](http://nbviewer.jupyter.org/github/marcotav/unsupervised-learning/blob/master/topic-modeling/notebooks/topic-modeling-lda.ipynb) ![image title](https://img.shields.io/badge/python-v3.6-green.svg) ![image title](https://img.shields.io/badge/ntlk-v3.2.5-yellow.svg) ![Image title](https://img.shields.io/badge/sklearn-0.19.1-orange.svg) ![Image title](https://img.shields.io/badge/pandas-0.22.0-red.svg) ![Image title](https://img.shields.io/badge/matplotlib-v2.1.2-orange.svg) ![Image title](https://img.shields.io/badge/gensim-0.3.4-blue.svg)

<p align="center">
  <a href="#intro"> Introduction </a> •
  <a href="#lib"> Libraries </a> •
  <a href="#pro"> Problem domain </a> •
  <a href="#cle"> Cleaning the text </a> •
  <a href="#docmatrix"> Document-term matrix </a> •
  <a href="#model"> LDA model </a>  •
  <a href="#pyLDAvis"> pyLDAvis </a>  •
  <a href="#results"> Results </a> 
</p>



<a id = 'intro'></a>
## Introduction
From Wikipedia:

> Network theory is the study of graphs as a representation of either symmetric relations or asymmetric relations between discrete objects. In computer science and network science, network theory is a part of graph theory: a network can be defined as a graph in which nodes and/or edges have attributes (e.g. names).

> Applications of network theory include logistical networks, the World Wide Web, Internet, gene regulatory networks, metabolic networks, social networks, epistemological networks, etc.; see List of network theory topics for more examples.


### Eulerian Path

An Eulerian path, is a path which crosses every edge *exactly* once. It exists if and only if:
- Every vertex has even degree
- Exactly two nodes have odd degree

The degree of a vertex is the number of edges incident to the vertex (loops count twice).


<br/>
<p align="center">
  <img src='images/euler-path.png' width="200">
</p>

### Types of Networks

- Undirected: connections extends in both directions.
- Directed: connections may only flow in one direction.
- Cyclic: contains at least one cycle (node can be connected to itself by traversing at least one edge).
- Acyclic: one that contains no cycles
- Multigraph: multiple links connecting the same pair of nodes.




### Importing libraries

Using the `networkx` library we can work with graphs.

import networkx as nx
from IPython.core.interactiveshell import InteractiveShell
InteractiveShell.ast_node_interactivity = "all" # see the value of multiple statements at once.
import matplotlib.pyplot as plt
%matplotlib inline

From the docs, `nx.Graph` is:
> A base class for undirected graphs. A Graph stores nodes and edges with optional data, or attributes. Graphs hold undirected edges.  Self loops are allowed but multiple (parallel) edges are not. Nodes can be arbitrary (hashable) Python objects with optional key/value attributes. By convention `None` is not used as a node. Edges are represented as links between nodes with optional key/value attributes.

The weight is a numerical value, assigned as a label to a vertex or edge of a graph. 

We can build a graph where all nodes are connected as follows:
```
nodes = ['A','B','C','D']
combs = [list((nodes[i],nodes[j])) for i in range(len(nodes)) for j in range(i+1, len(nodes))]
g = nx.Graph()

w = 0.1
for comb in combs:
    g.add_edge(comb[0],comb[1],weight=w)
    w += 1
nx.draw_networkx(g)
```