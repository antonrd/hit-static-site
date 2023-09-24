---
title: "Multiple dimensions"
type: docs
weight: 30
---
So far we illustrated the basic idea of dynamic programming - that the answer for a given problem can be computed using the answers for smaller sub-problems. We also showed that there is no need to compute the answer for the same sub-problem more than once and that we can store the computed answer and reuse it.

The Fibonacci problem was defined by only one dimension - the index of the number. However, dynamic programming can be applied to problems defined by more than one parameter. One very popular problem that can be solved using dynamic programming is the "0-1 Knapsack problem".

In this problem we have a set of `N` items each with a given weight and value (`W[i]` and `V[i]`). We are given a knapsack with a maximum capacity of `C`. Our goal is to select, which items to put into the knapsack, so that their total weight is not more than `C` and their total value is as large as possible.

To solve this task we need to define what a problem is and how one problem's answer can be computed using smaller sub-problems' answers.

Let's assume we order the items in some way, so that we have item 1, item 2, and so on. We can describe a problem with two parameters - the maximum capacity allowed and the highest index of an item to consider. These values for the final problem to solve are `N` for the highest index and `C` for the capacity. Now the question is: how do we break it down into smaller sub-problems?

For a given version of the problem described by some values `N` and `C` we have two options:

1. Put item with index `N` into the knapsack and reduce the capacity to `C - W[N]`
2. Don't put the item with index `N` into the knapsack and remain with capacity `C`

In the first case we will be interested in the answer for the problem with parameters `N-1`, `C - W[N]`. This answer will give us the maximum obtainable value when considering the first `N-1` items and limiting the total weight capacity to `C - W[N]`. To this answer we can add the value of item `N` since we decided to put it in the knapsack.

In the second case we will be interested in the answer for the problem with parameters `N-1`, `C`. This answer will give us the maximum obtainable value when considering the first `N-1` items and limiting the total weight capacity to `C`. To this answer we won't add any value because we have decided no to put item `N` into the knapsack.

Since we need to make a choice between adding and not adding item `N` into the knapsack, we should take the maximum between these two possible answers:

```
F(N, C) = max(F(N-1, C-W[N]) + V[N], F(N-1, C))
```

Here is our recursive dependency. Of course, we need to think about the base cases now.

The base values will be the all `F(1, *)` and `F(*, 0)`. The first are these for which we are only allowed to take the first item with any capacity in the range `[0, C]`. The second group are the sub-problems in which the maximum weight capacity is 0.

For `F(1, *)` we can say that the answer is 0 for these sub-problems in which the allowed capacity is less than `W[1]` and it is equal to `V[1]` for the rest of the cases in which the maximum capacity can hold item 1's weight.

For all `F(*, 0)` we know that the answer is 0 because there is no free capacity to hold any elements.

The answer that we are looking for is `F(N, C)`.

For the Fibonacci numbers we showed that the answer can either be computed by going "bottom-up" or "top-down". The first means that we start from the base cases and proceed to the final problem. In this task this would mean to first compute `F(1, *)`, then `F(2, *)`, `F(3, *)` and so on, until we reach `F(N, *)`. For this approach note that for computing `F(i, *)` we only need the values from `F(i-1, *)`. So, we don't need to store the earlier values all the time. This could help us save a lot of memory.

The second method, "top-down", would involve a recursive approach, in which we store and reuse the values once they are computed once. This is the memoization technique. Without it we would be computing the same value many times and this would make our solution quite inefficient.
