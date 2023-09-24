---
title: "Count the paths"
type: docs
weight: 20
---
### Task Statement

You are given a grid of cells with size `N` rows by `M` columns. A robot is situated at the bottom-left cell (row `N-1`, column `0`). It can move from cell to cell but only to the right and to the top. Some cells are empty and the robot can pass through them but others are not and the robot cannot enter such cells. The robot cannot go outside the grid boundaries.

The robot has a goal to reach top-right cell (row `0`, column `M-1`). Both the start and end cells are always empty. You need to compute the number of different paths that the robot can take from start to end. Only count paths that visit empty cells and move only to the right and up.

`N` and `M` will be numbers in the range `[1, 512]`.

Write a method, which accepts the grid as an argument and returns one integer - the total number of different paths that the robot can take from the start to the end cell, MODULO `1,000,003`. The reason we will use the modulo operation here is that the actual result could become a really big number and we don't want to let handling big numbers complicate the task more.

The input grid will contain `N` strings with `M` characters each - either `'0'` or `'1'`, with `'0'` meaning an empty cell and `'1'` meaning an occupied cell. Each of these strings corresponds to a row in the grid.

<hr/>

### Solution

This is another classic task, which can be solved efficiently using dynamic programming. The robot always starts at the bottom left cell. We need to figure out the parameters of the sub-problems. It is quite obvious that this can be the row and column of the cell to reach.

Once we compute this answer for the top row and right-most column we will have the answer to the whole task. Now, let's figure out the recursive relation between a problem and its sub-problems.

Once a robot is in a given cell `(x, y)`, there are two other cells, which it could have come from: `(x-1, y)` and `(x, y-1)`. Here we assume that the rows are numbered in increasing order from bottom to top and the columns are numbered in increasing order from left to right. Of course, we need to mention that for some cells there is only one cells from which the robot could have come. And for the start cell of the robot there are no cells from which it could have come there. For simplicity's sake let's assume below that there are two cells that lead to each cell. We will have to handle the edge cases in our implementation.

The above means that for each cell `(x, y)` there will be two types of paths that lead to it: the ones that pass through `(x-1, y)` and the ones that pass through `(x, y-1)`.

These two sets of paths have an empty intersection. So we can easily say that the answer for `(x, y)` can be computed the following way:

```
F(x, y) = F(x-1, y) + F(x, y-1)
```

The base case for our task is the number of paths that lead to the starting cell of the robot. Obviously, the answer for it is 1.

There is one more detail to mention. For the cells, which are occupied `F(x, y) = 0` because there are no paths leading to them, it's impossible to get to these cells.

As mentioned already in this section the solution could use one of the two techniques to compute the answers: bottom-up or top-down. If using bottom-up it will be easy to compute the answers row by row because each cell only needs one value from the row below it and one value from the same row. This would allow us to save on memory if that's needed. For our particular task where the maximum size of the board is 512x512 storing the whole board in memory is not such a big issue.

We could also implement a top-down solution, which recursively computes the values it needs on demand and stores the computed result for each cell in memory so it can be reused.

The time complexity of the described solutions is `O(N*M)` because for each cell we will compute the answer only once.
