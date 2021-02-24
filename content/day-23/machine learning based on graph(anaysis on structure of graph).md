# Machine Learning Based on Graph: Analysis on Structure

## 1. Structure of Community and Searching Community
### 1.1. definition of community
- a community $C$ is a set of vertices such that
  - for any $u, v \in C$, there exist a lot of edges between them
  - for $u \in C, v \notin C$, there exist few edges between them
  - it is not a mathematical definition

### 1.2. community of real graph
- communities in SNS usually mean social circles
- some communities in SNS have something with fraud, cheating or something like crime
- division within a group can be expressed as communities of SNS
- in a graph consisting of (keyword, advertiser), keywords with a same theme form a cluster

### 1.3. community detection problem
- the way to divide vertices into clusters properly is called "Community Detection"
- in general, one node belongs to only one cluster
- "Community Detection" is similar with "Clustering", one of unsupervised machine learning task
- first of all, we need to define a sucessful community detection

## 2. Statistical Significance of Community
### 2.1. configuration model
- for given $G$, the configuration model is a graph such that
  - for all node, the degree of the node does not change
  - edges of $G$ are rearranged randomly
- in a configuration model, the probability of occurence of a edge between $i$ and $j$ is proportional to the connectivity between them


### 2.2. definition of clustering
- to decide whether community detection works well or not, modularity will be considered
  - suppose that $G$ and $S$, a set of clusters, is given
  - for each $s\in S$, the difference of the number of edges of $s$ within $G$ and within a configuration model of $G$ is calculated<br>
  $G$: graph<br>
  $S$: a set of clusters<br>
  $$
  \frac{1}{|E|} \sum_{s\in S} \left[\#(edge_{in}(s)) - mean(\#(edge_{in}(s_{config}))) \right]
  $$
  - as modularity increases, community detection works well


## 3. Community Detection Algorithm
### 3.1. Girvan-Newman algorithm
- Girval-Newman algorithm is a top-down community detection algorithm
- process
  1. for each edge in $G$, calculate betweeness
  2. remove the edge which has the smallest value of betweeness
  3. calculate a modularity
  4. till the modularity becomes optimal, repeat (1)~(3)

### 3.2. Louvain
- Louvain algorithm is a bottom-up community detection algorithm
- process
  1. each node forms a community(singleton)
  2. for each $u$ in $V(G)$, move to a new community or existing community for a modularity to increase
  3. till the modularity becomes optimal, repeat (1), (2)

## 4. Community Detection with Overlapping
### 4.1. communities with overlapping
### 4.2. nested community model
### 4.3. relaxed nested community model

## 5. Practice