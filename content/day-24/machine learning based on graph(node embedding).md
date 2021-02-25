# Machine Learning Based on Graph: Node Embedding

## 1. Node Embedding Learning
### 1.1. what is node embedding?
- Node Embedding is an expression of nodes as vectors
- vector space which node embedding vectors belong to is called a embedding space

### 1.2. why node embedding?
- techniques appliable to vectors can be applied to methods for graph
- ex. logistic regression, multi-layer perceptron, K-means, DBSCAN can be applied to graph
- ex. tasks like node classification, community detection can be conducted by using DL, ML

### 1.3. goal of node embedding
- node embedding should preserve similarity of nodes
- in embedding space, similarity of nodes is defined as
  $$
  similarity(u, v) \eqsim {\mathbf{z}_v}^T\mathbf{z}_u
  $$
- in summary, node embedding consists of two steps
  1. define similarity of nodes in graph
  2. learn embedding to preserve similarity of nodes in graph

## 2. Approach Based on Adjacency
### 2.1. approach based on adjacency
- key idea:<br>if $u, v$ are adjacent, $z_u$ and $z_v$ are similar
- loss function:<br>
  $$
  \mathcal{L} = \sum_{(u, v)\in V\times V}{||z_u^Tz_v-A_{u, v}||}^2
  $$
  where $A_{u, v}$ is $(u,v)$ element of the adjacent matrix $A$

### 2.2. limitation
- for $u, v \in E(G)$, if $d(u,v)$>1, then $A_{u,v}=0$
- this approach also loses the information of community

## 3. Approach Based on Distance, Path and Overlapping
### 3.1. approach based on distance
- similarity is high if the distance between them is small

### 3.2. approach based on path
- similarity is proportional to the number of pathes between two nodes
- path from $u$ to $v$ is a sequence of nodes such that
  1. it starts with $u$ and ends with $v$
  2. for every consecutive pairs in path, there exists an edge between them
- loss function:<br>
  $$
  \mathcal{L} = \sum_{(u, v)\in V\times V}{||z_u^Tz_v-A_{u, v}^k||}^2
  $$
  where $A$ is the adjacent matrix

### 3.3. approach based on overlapping
- similarity is proportional to the size of intersection of neighborhoods
- terms: for $u, v \in E(G)$<br>
  $N_u(=N(u))$: the neighborhood of $u$<br>
  $S_{u, v}=|N_u\cap N_v|=\sum_{w\in N_u\cap N_v}1$
- loss function:<br>
  $$
  \mathcal{L}=\sum_{(u, v)\in V\times V}{||z_u^Tz_v-S_{u, v}||}^2
  $$
- we can use Jaccard similarity or Adamic adar score as similarity instead of $S_{u, v}$<br>
  Jaccard similarity: $\frac{|N_u \cap N_v|}{|N_u \cup N_v|}$<br>
  Adamic adar score: $\sum_{w \in N_u \cap N_v}\frac{1}{d_w}$ 


## 4. Approach Based on Random Walk
### 4.1. approach based on random walk
- the probability that $u$ reaches $v$ while walking randomly through edges is considered as similarity
- process
  1. for each node, start random walk from the node and repeat
  2. define the collection of nodes which were encountered during random walk with duplication as $N_R(u)$
  3. learn embedding to minimize the loss function suggested below:<br>
  $$
  \mathcal{L} = \sum_{u \in V} \sum_{v\in N_R(u)}-log(P(v|z_u))
  $$


### 4.2. deepwalk and node2vec
- deepwalk uses the random walk introduced before(uniform probability of walk)
- node2vec uses second-order biased random walk
- in second-order biased random walk, there are 3 directions
  1. distance-preserving direction
  2. direction toward previous node
  3. direction away from previous node
- the probabilities of direction have distinct values
- if the probability of 3 > the probability of 2<br>each cluster has nodes with similar property
- if the probability of 3 <> the probability of 2<br>each cluster has nodes within a same community


### 4.3. loss function approximation
$$
\mathcal{L} = \sum_{u \in V} \sum_{v\in N_R(u)}-log(P(v|z_u))
$$
- the original loss function is expensive to optimize embeddings
- negative sampling
- using sigmoid
  $$
  log(\frac{exp(z_u^Tz_v)}{\sum_{n\in V}exp(z_u^Tz_n)}) \\
  \simeq log(\sigma(z_u^Tz_v))-\sum_{i=1}^{k}log(\sigma(z_u^Tz_{n_i}))
  $$
  where $n_i \sim P_V$


## 5. Limitation of Node Embedding Learning
### 5.1. transductive and inductive
- transductive gives embedding as a result
- inductive gives an encoder as a result


### 5.2. limitation
- transductive
  - after learning, unknown input can not be embedded
  - all embedding for each node should be calculated and saved
  - attributes of node are not usable

## 6. Practice (Node2Vec)