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

Creating an adjacency list is a verry common way of representing graphs. In this representation, each node *x* is assigned to a list of other nodes that *x* is connected to 

*x* -> [*y*, *z*, ...] and *y* -> [*x*, ...] for an undirected graph

The benefit of using adjacency lists is that we can efficiently find the nodes
to which we can move from a given node through an edge. Adjacency lists are of size *n* where *n* is the number of nodes in the graph.

**Pros:** Saves space O(|V|+|E|) . In the worst case, there can be C(V, 2) number of edges in a graph thus consuming O(V^2) space. Adding a vertex is easier.

**Cons:** Queries like whether there is an edge from vertex u to vertex v are not efficient and can be done O(V).

### Adjacency Matrices

An adjacency matrix is a 2D array that contains which edges the graph contains. Using this, we can check if there is an edge between two nodes in 
constant time. 

**Example:**

```JavaScript
const adjMatrix = [
    [0, 1, 0],
    [1, 0, 1],
    [0, 1, 0]
]

// adjMatrix[0][1] = 1, which means there's an edge between nodes 0 and 1
```

For an unweighted graph, the adjacency matrix can be of boolean type or contain 0s and 1s as the values in each index. If the
graph is weighted then each index into the graph can be the weight of that respective edge.

**Pros:** Representation is easier to implement and follow. Removing an edge takes O(1) time. Queries like whether there is an edge from vertex ‘u’ to vertex ‘v’ are efficient and can be done O(1).

**Cons:** Consumes more space O(V<sup>2</sup>). Even if the graph is sparse(contains less number of edges), it consumes the same space. Adding a vertex is O(V<sup>2</sup>) time.
