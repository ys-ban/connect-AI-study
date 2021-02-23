# Machine Learning Based on Graph: Marketing
## 1. Propagation through Graph
### 1.1. information propagation through graph
- a lot of information spreads out through SNS
- ex) political issues

### 1.2. behavior propagation through graph
- a lot of behaviors spreads out through SNS
- ex. ice bucket challenge, penguin profile pic, etc.

### 1.3. trouble(breakdown) propagation through graph
- a lot of breakdown spreads out through SNS
- ex. breakdown of computer network, electric shutdown

### 1.4. disease propagation through graph
- a lot of diseases spreads out through SNS
- ex. SARS, COVID-19, Mers

-----------

- processes of propagation not only vary widely but also is too complicated
- to deal with them, we need mathematical modeling
- in this course, two models will be introduced among many models and methods
-----------

## 2. Propagation Model Based on Decision Making
### 2.1. when does propagation model based on decision making be used?
- in 1970's, there were two kinds of videos, VHS and betamax
- recently, there are two main communication applications, kakao talk and line
- we used to choose one of options according to the choices of people arround us
- in this case, propagation model based on decision making can be used

### 2.2. linear threshold model
- make a situation mathematically abstract:
  - assume that there are $u$ and $v$ who are friends
  - the two will choose either $A$ or $B$ which are not compatible
  - if both of them chooses $A$, the benefit will increase by $a$
  - if both of them chooses $B$, the benefit will increase by $b$
  - if they choose different one respectibly, the benefit will not change
  - in social network, one compares benefits while making decision 
  $$
  p := the\; proportion\; of\; A \\
  1-p := the\; proportion\; of\; B
  $$
  - if $ap>b(1-p)$, then $A$ will be chosen
  - equivalently, if $p> \frac{b}{a+b}$, $A$ will be chosen
  - in this case, we call $\frac{b}{a+b}$ a threshold
  

## 3. Probabilistic Propagation Model
### 3.1. when does probabilistic propagation model be used?
- progation model based on decision making does not fit with COVID-19 case
- because anyone does not decide to get sick of COVID-19
- COVID-19 propagation is probabilitistic, stochastic process


### 3.2. independent propagation model
- make COVID-19 propagation mathematically abstract:
  - COVID-19 propagation is probabilitistic, stochastic process
  - assume directed and weighted graph $G$
  - a weight $p_{uv}$ is the probability for uninfected $v$ get COVID-19 by infected $u$
  - for different $u,v,w$, $p_{uv}$ and $p_{uw}$ is independent
  - the end condition is the case where there is no one to get infected
  - suppose that the infected sustain infected
    - there are models where the infected can be cured like SIS, SIR


## 4. Viral Marketing and Influence Problem

### 4.1. what is viral marketing
- viral marketing is a business strategy that uses existing social networks to promote a product
- to be effective, the start point matters
- the range of speading out depends on start point
- that's why social influencers pay a lot


### 4.2. the importance of seed set
- one of popular social influencers is Kate Middleton, the wife of british prince William
- "Kate Middleton effect"
- in models suggested before, seed sets also matter

### 4.3. influence maximization problem
- influence maximization problem is a problem to find the seed set which maximizes propagation for given graph, propagation model, size of seed set
- influence maximization problem is very hard
  - for given $G = (V, E)$ and seed size = $k$, the number of cases is $\left( \begin{matrix} |V| \\ k \end{matrix} \right)$
  - if $|V| = 10000, \; k=10$,
  $$
  \#\;of\;cases\;\eqsim \;2.7\times 10^{33}
  $$
  - theoretically, a influence maximization problem is NP-hard for many models
- therefore, we need to another strategies to find a proper seed set(not best seed set)

### 4.4. heuristics of vertex centrality
- one of popular heuristics uses node centrality
  - for given seed size $k$, choose $k$ nodes in order of centrality
  - use pagerank score, connectivity, closeness and betweeness as node centrality
- it seems resonable but there is no gaurantee of finding the best and optimal seed set

### 4.5. greedy algorithm
- greedy algorithm is also used
  - in greedy algorithm, a member of seed set is chosen once at a time
  - a member is selected to maximize an influence
  - till the size of selected seed set is equal to the size as we expected, repeat iteration
- accuracy of greedy algorithm
  - in an independent propagation model, the accuracy is guaranteed to some extent
  - $S_{chosen}$: the average of sizes of seed set obtained by greedy algorithm<br>$S_{optm}$: the average of sizes of the best seed set
  $$
  S_{chosen} \geq (1- \frac{1}{e})S_{optm}
  $$

## 5. Practice

```{python}
import networkx as nx
import matplotlib.pyplot as plt
import random

import os
import os.path as osp
from google.colab import drive
```

```{python}
cd ./drive/MyDrive/Colab\ Notebooks
```

```{python}
G = nx.DiGraph()
path_data = './data/lab/lab4/simple_weighted_directed_graph.txt'

f = open(path_data)
for line in f:
  line_split = line.split()
  src = int(line_split[0])
  dst = int(line_split[1])
  w = float(line_split[2])
  G.add_edge(src, dst, weight = w)
```

```{python}
def draw(G: nx.Graph, affected: set(), used: set()) -> None:
    pos = {
            0:[0.5, 0.8], 1: [0.1, 0.5], 2:[0.2, 0.2],
            3:[0.8, 0.7], 4: [0.7, 0.4], 5:[0.45, 0.45],
            6:[0.6, 0.1], 7:[0.9, 0.35], 8:[0.7, 0.1]
    }
    
    nodeColorList = []
    nodeList = []
    for i in range(len(G.nodes)):
        nodeList.append(i)
        if i in affected:
            nodeColorList = nodeColorList + ['red']
        else :
            nodeColorList = nodeColorList + ['blue']
    im = nx.draw_networkx_nodes(G, pos, nodelist = nodeList, node_color=nodeColorList, node_size=100)
    edgeList = []
    edgeColorList = []
    for edge in G.edges:
        edgeList.append(edge)
        if edge in used:
            edgeColorList = edgeColorList + ['red']
        else :
            edgeColorList = edgeColorList + ['blue']
    nx.draw_networkx_edges(G, pos, edgelist = edgeList, edge_color = edgeColorList)
    nx.draw_networkx_labels(G, pos, font_size=10, font_color="black")
    plt.show()

```

```{python}
affected = set()
affected_new = set({0})
used_edge = set()

while len(affected_new)!=0:
  draw(G, affected_new, used_edge)
  temp = set()
  for src in affected_new:
    neighbor = G.neighbors(src)
    for dst in neighbor:
      if (dst not in affected) and (dst not in affected_new):
        p = random.uniform(0,1)
        if p<G.edges[src, dst]["weight"]:
          temp.add(dst)
        used_edge.add((src, dst))
  affected = affected | affected_new
  affected_new = temp
draw(G, affected_new, used_edge)
```
