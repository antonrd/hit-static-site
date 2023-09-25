---
title: "Traversals"
type: docs
weight: 20
aliases: ["/classrooms/algorithm-design/lesson/47"]
---
Graph traversals are a very popular set of problems in which some entity is represented by a graph and the nodes in this graph need to be traversed in some order. Sometimes one needs to find if there is a way to get from node `Vi` to another node `Vj` following the existing edges in the graph. Two popular algorithms for this are Depth-first search (DFS) and Breadth-first search (BFS). After learning and practicing the different representations of graphs these two algorithms are a must for people learning to code graph algorithms.

In summary, DFS is about starting from one node and recursively continuing to the nodes that are connected to it by edges and have not yet been visited by the traversal.

The idea of BFS is different, starting from a node it first visits all its neighbours and then does the same for all of them in some order.

On one hand these algorithms both traverse the edges of a graph that are reachable from the starting node. On the other hand, due to the different traversal strategies, these two algorithms have their pros and cons.

### Depth-first search

As mentioned above DFS takes a somewhat recursive approach, a simple pseudocode will look like that:

```ruby
def dfs(node)
  mark node as visited

  for next_node in neighbours(node)
    if not visited(next_node)
      dfs(next_node)
    end
  end
end
```

If implementing it recursively you need to be aware of the stack depth. If, for example, the graph is like a chain of nodes consecutively connected by edges and the number of nodes is high enough your program may crash due to consuming too many stack frames. Of course, it is possible to avoid this problem by implementing the recursive approach iteratively.

The time complexity of DFS is `O(N+M)` where `N` is the number of nodes and `M` is the number of edges. If the graph is connected calling the `dfs` function on node should suffice to traverse all nodes. If the algorithm is executed on a graph that may have multiple disconencted components, then it will make sense to call the `dfs` function on all nodes in it to make sure that all disconected components are traversed. During interviews it's especially important to consider these specifics of the problem. If they are not clear, make sure to ask and clarify the situation. This will help you design and implement a correct algorithm.

As was mentioned above, if you impement your DFS with recursion, you need to be careful about stack overflows. This is a major issue if the input graph can be, for example, a very long chain of nodes that will create a large number of nested stack frames. Ackowleding this problem at an interview is a great sign that you are thinking of various edges cases and extreme situations.

### Breadth-first search

With BFS the solution is usually implemented using a queue and is iterative. There is one very useful effect of running BFS - when starting from a given node, it will get to all reachable nodes with the minimum possible number of hops (edges). This is useful in problems in which one needs to find the minimum path in terms of edges between two or more nodes in a graph.

This is pseudocode for BFS:

```ruby
def bfs(node)
  queue.add(node)
  mark node as visited
  distance[node] = 0

  while not queue.empty
    top_node = queue.pop
    for next_node in neighbours(top_node)
      if not visited(next_node)
        queue.add(next_node)
        mark next_node as visited
        distance[node] = distance[top_node] + 1
      end
    end
  end
end
```

The time complexity of BFS is `O(N+M)` where `N` is the number of nodes and `M` is the number of edges. Like with DFS above, if the graph consists of disconnected components calling the `bfs` function on all nodes to ensure that all are visited would be needed.

We encourage you to read more about these algorithms and you will also have a chance to apply them in the practice tasks in this section.
