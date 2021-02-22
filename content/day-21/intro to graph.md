# Intro to Graph
## what is graph
### basic definition of graph
- Graph (V, E) is a mathematical structure which consists of a set of vertices and a set of edges
- an edge is a kind of a bridge between two vetices
- graph is called network alse
### why is graph important
- complex system
- the reason a complex system is complex is a lot of interations between components of complex system
- graph is a language for expressing and analysing components and interactions of complex systems
- (customer, product), (user, user), and so on
- so to understand and predict complex system, we have to learn graph
## AI problem
### node classification
- predict a political position of some tweeter user
- figure out a role of protein
### link prediction
- how facebook network evolute
### recommendation
- which node need product A?
### community detection
- how can we find a meaningful social circle from data of edges?
### ranking and information retrieval
- how can we find important web pages from network of web?
### information cascading and viral marketing
- how the information go viral
- how the information spread out
### coverage of this course
- it covers AI techniques about problems suggested before
- it focuses on intuitions and intuitive methods rather than high-end techniques
- but some of high-end techniques about graph will be introduced(graph neural network)

## concept
### types of graph
- undirected graph
  - graph (V, E) is said to be undirected if every edge in E has no direction
  - ex) cooperation graph, relationship at facebook
- directed graph
  - graph (V, E) is said to be directed if every edge in E has direction
  - ex) quotation graph, tweeter following-follower graph

------

- unweighted graph
  - graph (V, E) is said to be unweighted if it is not weighted
  - ex) web, facebook friend
- weighted graph
  - graph (V, E) is said to be weighted if there exists a weight for each edge of E
  - ex) calling graph, similarity graph

------

- unbipartite graph
  - graph (V, E) is said to be unbipartite if every vertex of V has a same type
- bipartite graph
  - graph (V, E) is said to be bipartite if there exist only two types of node

------

- what type of graph the interactions of e-commercial has?
  - undirected, weighted, bipartite

------

- neighbor
  - a set of vertices which are connected directly with $v$ is called a neighbor of $v$, denoted by $N(v)$
- if a graph $G$ is directed, $N(v)$ is splitted into $N_{out}(v)$ and $N_{in}(v)$



## expression

### Python library **NetworkX** Usage(basic)

```{python}
import networkx as nx
import numpy as np
import matplotlib.pyplot as plt


print("##### create graph #####")

G = nx.Graph()
DiG = nx.DiGraph()


print("##### add node to graph #####")
G.add_node(1)
print(f"num of nodes in G: {G.number_of_nodes()}")
print(f"graph: {G.nodes}")


print("##### add vertox 2~10 #####")

for i in range(2, 11):
  G.add_node(i)
print(f"num of nodes in G: {G.number_of_nodes()}")
print(f"graph: {G.nodes}")

print("##### add edge #####")
for i in range(1, 11):
  G.add_edge(1, i)
print(f"graph: {G.edges}")


# visualization
pos = nx.spring_layout(G)
im = nx.draw_networkx_nodes(G, pos, node_color="red", node_size=100)
nx.draw_networkx_edges(G, pos)
nx.draw_networkx_labels(G, pos, font_size = 10, font_color="black")

plt.show()
```


### expression for graph and export as a file

- edge lis
- adjacent list
- adjacency matrix


## Real Graph vs Random Graph
- real graph is a graph obtained from the real data of complex system
- random graph is a graph made by some mathematical, stochastic process
- Erdös-Rényi random graph
  - denoted by $G(n, p)$
  - there exist $n$ vertices
  - a probability of existence of edge for any pair of vertex $(x, y)$ is $p$
  - and the probability is independent

## Small World Effect
- a path from $u$ to $v$ is a sequence of vertices satisfying
  - it starts with $u$
  - it ends with $v$
  - for each $x$ of a path, there exists an edge from $x$ to the consecutive of $x$
- a length of a path is the number of edges which are contained in the path
- a diameter of $G$ is the maximum of all length of path
- a dictance from $u$ to $v$ is the length of the shortest path from $u $ to $v$
- the mean of distances for pairs of vertices in real graph is close to 6(quite small)
- but is is not the case of chain, cycle, grid graphs

## Heavy-tailed Distribution of Connectivity
- a degree of a vertex $u$ is a size of the neighbor of $u$
- in directed graph, a in-degree of a vertex $u$ is a size of the in-neighbor of $u$
- in directed graph, a out-degree of a vertex $u$ is a size of the out-neighbor of $u$
- a connectivity of real graph follows heavy-tailed distribution
  - probably, there exist hubs
- a connectivity of random graph follows normal distribution
  - probably, there exists no hub

## Giant Connected Components
- in real graph, there exists a giant connected component
- in random graph with mean connectivity less than 1, there exists no giant connected component
- in random graph with mean connectivity biger than 1, probably there exists a giant connected component

## Community
- Local clustering coefficient
- Global clustering coefficient
