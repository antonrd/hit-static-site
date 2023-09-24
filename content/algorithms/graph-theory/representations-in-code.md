---
title: "Representations in code"
type: docs
weight: 10
---
In order to code graph algorithms one needs to know how to represent them in memory. There are some more widely used representations and each one has advantages and disadvantages compared to the others. Hence, it's good to know which one to use for a given problem. This may be a crucial decision for an interview problem.

One popular representation is a matrix `M` with size `n x n` where `n` is the number of nodes in the graph. The cell `M[i][j]` will contain a value indicating whether there is an edge going from node `i` to node `j`. This representation will work for graphs with or without weights on their edges. It will also work for graphs with or without directed edges. Of course, for undirected graphs the matrix will be symmetric because `M[i][j] = M[j][i]` for all `i, j`.

The matrix representation takes `O(n^2)` memory, which may not be optimal in some cases but it could turn out to be very fast to use for certain algorithms. Also, for dense graphs (with many edges) this representation may happen to have similar memory usage as other representations.

Another representation is one, which has a list of neighbours for each node. This means that for each node `Vi` in a graph `G` we will have to store the identifiers of the nodes, which are connected to `Vi` by an edge. With this representation you could save a lot of memory compared to the matrix approach for sparse graphs in which the consumed memory will be `O(m)` where `m` is the number of edges in the graph.

Finally, one more representation that could be useful in some cases is a list of edges. This means that you would just store a list of all edges as pairs of nodes and the attributes associated with each edge. This would again require memory that is `O(m)` but could be more suitable for a limited set of problems.

Now let's look at some popular classes of graph algorithms.
