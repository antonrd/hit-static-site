---
title: "Network connectivity"
type: docs
weight: 20
aliases: ["/classrooms/algorithm-design/lesson/36"]
---
### Task Statement

The computers in one company's head quarters are connected by a local area network. However, due to various restrictions not all computers may be reachable from all other computers in the building.

The system administrators of the building have a list of all connections between nodes on the network (computers and network devices). The list consists of pairs of numbers where each number is the assigned ID of a node on the network. The connections allow for communication in both directions.

Your task is to write a program, which can be used to determine how many network nodes are reachable from a given node with ID `S`.

The network has `N` nodes where `1 <= N <= 512`.

The input is read from the standard input. On the first line there will be three integers `N` - the number of nodes, `M` - the number of connected pairs of nodes and `S` - the ID of the node which we are asking the question for. Then `M` lines will follow each containing two integers - IDs of network nodes. The IDs will be in the range `[1, N]`.

The output is written to the standard output. It must contain only one integer - the number of network nodes reachable from the node with ID `S`.

**SAMPLE INPUT**

```
7 8 2
1 2
1 4
4 2
4 3
3 1
5 6
5 7
7 6
```

**SAMPLE OUTPUT**

```
3
```

The nodes reachable from the node with ID `2` are `1, 3, 4`. The other nodes are not connected in any way to the node with ID `2`.

<hr/>

### Solution

This is a classical graph task requiring you to find all nodes in a graph that are reachable by a given node. Some things to figure out before starting to design you solution are:

- What characteristics the graph has?
- How big can the graph be in terms of nodes and edges?

#### Graph characteristics

This graph has bi-directional edges meaning that you could "travel" in both directions of each edge. If node `A` is reachable by node `B` then the opposite will also be true.

The task statement doesn't mention if there could be multiple edges between two nodes. However, this is pretty much irrelevant because we only care if two nodes have at least one edge between them.

It is also not clear if a node can have an edge to itself. True or not, this is also not  important because we don't count the starting node itself in the final answer.

Still, at an interview it's ok to ask about these things in order to be clear about what to expect.

#### Graph size

The statement says that the graph can have at most `512` nodes. There is no limit for the edges. There are `N * (N - 1) / 2` possible edges in the graph. The input could mention the same edge more than once in theory but as mentioned above we shouldn't count the same edge more than once.

#### Possible solutions

This task can be solved by running a simple traversal, like the ones mentioned in the overview lessons of this section. We could consider DFS or BFS for this purpose. With DFS, as we mentioned before, we should be careful because of its recursive nature. If you implement it using a recursion it could in theory create as many stack frames as there are nodes in the graph. If the graph is big enough this could lead to stack overflows depending on the programming languages, compiler, interpreter and so on. So, the BFS implementation is safer in this regard.

However, the maximum size of the graph is `512` nodes and this should not be causing issues with the stack even if we use DFS. It's good to always have this potential problem in mind and maybe discuss it briefly with the interviews.

If you apply DFS, it must start from the node `S` as defined in the task statement. It will traverse all reachable nodes and all you need to do is count the different visited nodes.

In a very similar fashion, when using BFS, first you put the node `S` on the queue and let the traversal visit all reachable nodes. Count every new node that gets inserted in the queue.

Here is a sample solution using DFS written in Ruby:

```ruby
def dfs(node, nei, vis)
  return 0 if vis[node]

  res = 1
  vis[node] = true
  nei[node].each do |nn|
    res += dfs(nn, nei, vis)
  end

  res
end

n, m, s = gets.strip.split.map(&:to_i)

nei = Array.new(n+1) { [] }

m.times do
  from, to = gets.strip.split.map(&:to_i)
  nei[from] << to
  nei[to] << from
end

puts dfs(s, nei, Array.new(n+1, false)) - 1
```

And this is a solution using BFS written in C++:

```cpp
#include <iostream>
#include <vector>
#include <queue>

using namespace std;

int n, m, s;
vector<int> neighbours[513];
vector<bool> vis(513, false);

int main() {
  cin >> n >> m >> s;

  for (int i = 0; i < m; i++) {
    int from, to;
    cin >> from >> to;
    neighbours[from].push_back(to);
    neighbours[to].push_back(from);
  }

  queue<int> q;
  q.push(s);
  vis[s] = true;
  int result = 0;

  while (!q.empty()) {
    int node = q.front();
    q.pop();

    for (vector<int>::iterator it = neighbours[node].begin(); it != neighbours[node].end(); ++it) {
      if (!vis[*it]) {
        vis[*it] = true;
        q.push(*it);
        result++;
      }
    }
  }

  cout << result << endl;

  return 0;
}
```
