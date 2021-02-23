# Machine Leaning Basaed on Graph: Pagerank
## 1. Background of Pagerank
 ### 1.1. web and graph
  - web is a big directed graph composed of webpages and hyperlinks
  - webpages are vertices
  - hyperlinks are edges
  - webpages contain keyword iinformation additionally
 ### 1.2. search engine before google
 1. arrange web as one big directory
 2. search engine dependent on keywords which are contained in a webpage
## 2. Definition of Pagerank
 ### 2.1. definition of pagerank: in aspect of voting
 - key idea of pagerank is voting
 - voter is webpage
 - webpage votes by hyperlink
 - using voting, find webpages that are highly reliable and relevant with keywords given by users
 - if webpage A contained a hyperlink connected with webpage B, the author of A may think that B is highly reliable and relevant with A
 - it means that in-degree is proportional to connectivity
 - but some user can cheat
 - so to prevent this kind of fraud, each voting should have the weight respectively
 - to calculate this score, use iteration(fixed-point problem)
  $$
  r_j = \sum_{i \in N_{in}(j)} \frac{r_i}{d_{out}(i)}
  $$
 ### 2.2. definition of pagerank: in aspect of random-walk
 - assume that web surfer walk randomly along webs
 - web surfer goes to the next webpage with $p$ which follows a uniform distribution
 - let $p_i(t)$ be the probability that websurfer visits webpage $i$ at time step $t$
 - then canonically
  $$
  \mathbb{p}(t) = (p_1(t), p_2(t), \dotsb, p_n(t)) \\
  p_j(t+1) = \sum_{i \in N_{in}(j)} \frac{p_i(t)}{d_{out}(i)}
  $$
 - if $p$ converges(it means stationary distribution),
  $$
  p_j = \sum_{i \in N_{in}(j)} \frac{p_i}{d_{out}(i)}
  $$

## 3. Calculation of Pagerank
### 3.1. calculation of pagerank: iteration
1. initialize $r_i^{(0)} = \frac{1}{|V|}$
2. udpate by the iteration below
   $$
   r_j^{(t+1)} = \sum_{i \in N_{in}(j)} \frac{r_i^{(t)}}{d_{out}(i)}
   $$
3. till converge(if diff < tol), repeat the iteration
### 3.2. obstacles and breakthroughs
- obstacles

    1. is the convergence always guaranteed?
        - no, there exists a spider trap problem(connected components result in, $N_{in}(V)\neq \phi, N_{out}(V)= \phi$ )
    2. is the result of iteration always reliable?
        - no, there exists a problem caused by dead end($N_{in}(u)\neq \phi, N_{out}(u)= \phi$)

- breakthroughs

  1. the concept of teleport is introduced
  2. damping factor is introduced

- modified assumption of surfer's behavior
  1. if there is no hyperlink, a surfer teleports to a random webpage
  2. if there are hyperlinks, a surfer tosses a coin
  3. if head comes, the surfer goes to one of webpages connected with hyperlinks
  4. if tail comes, the surfer teleports to a random webpage

- modified version of iteration
  $$
  r_j^{(t+1)} = \sum_{i \in N_{in}(j)} \alpha \frac{r_i^{(t)}}{d_{out}(i)} + (1-\alpha)\frac{1}{|V|}
  $$

## 4. Practice

```{python}
import networkx as nx
import numpy as np
import matplotlib.pyplot as plt
import os
import os.path as osp
import sys
```

```{python}
# the code below depends on the environment where you work

ls
cd ./drive/MyDrive/Colab\ Notebooks
cd ./data/

path_v2n = './others/vertex2name.txt'
path_edges = './others/edges.txt'
path_keyword = './lab/lab3/deep_learning.txt'
```

```{python}
G = nx.DiGraph()

f = open(path_edges)
for line in f:
  v1, v2 = map(int, line.split())
  G.add_edge(v1, v2)
f.close()

n2v = {}
v2n = {}
f = open(path_v2n)
for line in f:
  v, n = line.split()
  v = int(v)
  n = n.rstrip()
  n2v[n] = v
  v2n[v] = n
f.close()

node_key = []
f = open(path_keyword)
for line in f:
  v = line.rstrip()
  v = int(v)
  node_key.append(v)
f.close()
```

```{python}
H = G.subgraph(node_key)
```

```{python}
pr = nx.pagerank(H, alpha = 0.9)
res = [key for (key, value) in sorted(pr.items(), key = lambda x : x[1], reverse = True)]
for item in res[:10]:
  print(f"vertex: {item}\t\tkey: {v2n[item]}\t\tpagerank: {pr[item]}")
```

