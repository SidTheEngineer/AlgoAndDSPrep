## Graphs

### Terminology
- **Connected** - A graph is connected if there is a path between any two nodes.
- **Components** - The connected parts of a graph
- **Tree** - A connected graph that consists of *n* nodes and *n* - 1 edges.
- **Simple** - A path is simple if each node appears at most once in the path.
- **Degree** - The degree of a node is th number of its neighbors
- **Regular** - A graph is regular if the degree of every node is a constant *d*.
- **Complete** - A graph is complete if the degree of every node is *n* - 1,
- **Indegree** - In a directed graph, the indegree of a node is the number of edges that end at the node.
- **Outdegree** - In a directed graph, the outdegree of a node is the number of edges that start at the node.

### Adjacency Lists

Creating an adjacency list is a verry common way of representing graphs. In this representation, each node *x* is assigned to a list of other nodes that *x* is connected to (e.g *x* -> [*y*, *z*, ...] and *y* -> [*x*, ...] for an undirected graph). The benefit of using adjacency lists is that we can efficiently find the nodes
to which we can move from a given node through an edge. Adjacency lists are of size *n* where *n* is the number of nodes in the graph.

### Adjacency Matrices

