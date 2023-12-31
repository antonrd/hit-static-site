---
title: "Memory complexity"
type: docs
weight: 30
aliases: ["/classrooms/algorithm-design/lesson/50"]
---
To measure memory complexity of a solution you can use a lot of the things that we already described in this section. The difference is that here you need to measure the maximum amount of memory that is used by your solution at one point in time. Why is that important? Mainly because every time you run a piece of software on a given machine you will only have a limited amount of memory. Go over this amount and you are in trouble. The first most likely effect will be that the OS will start to swap memory to hard disk, which will make the execution much slower and practically useless.

Hopefully, you agree that memory usage is as important as the running speed of an algorithm. You can measure it in similar ways to how you measure the time complexity. For example, let's look again at the example with the permutations of latin letters. First, to hold all the letters you will need memory proportional to `N` (the number of letters). Then, to generate all permutations you could use the same array and just generate subsequent permutations in it. Checking if a sequence of letters is a palindrome does not require additional memory. We could say that this brute force solution requires memory proportional to `N`. In terms of memory usage this solution is not bad then.

Let's look at another example. Consider a task in which you need to store information about a network of some kind. The network has nodes and edges that connect them. We will look at more tasks like this one in the section covering graphs but in this lesson let's just focus on how we could represent the network in memory.

One way would be to store a square matrix `M` with size `N x N` where `N` is the number of nodes in the network. In each cell `M[i][j]` we will have 0 or 1 indicating if there is an edge between nodes `i` and `j`. This representation of the network requires that we use memory proportional to `N^2`.

An alternative approach would be to store for each node a list of the nodes that it is connected to. In this case we can allocate memory that is proportional to the number of edges in the network. If nothing else is specified the number of edges could vary from 0 to `N * (N-1)`. This means that in the worst case the memory used will also be proportional to `N^2`, like for the previous representation. But if for example we know that the network is quite sparse and doesn't have many edges, the memory used will be less that what we would consume with the first approach. We can even go further and define the memory usage in terms of the number of nodes `N` and the number of edges `M`. Let's say that the lists are stored in a hashmap where the key is some label for a given node and the value is a list of other nodes to which it has edges. Then, this hashmap will have keys for the nodes that have edges connected to them and for each edge in the network there will be one entry, which is inside a list stored as a value in the hashmap. This means that the memory complexity is proportional to the number of edges `M`.

When designing a solution for a problem at a tech interview you will need to be able to compute the memory complexity, so that you can explain to the interviewer why a solution is good or bad given the input constraints.
