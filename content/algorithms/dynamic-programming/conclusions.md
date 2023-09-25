---
title: "Conclusions"
type: docs
weight: 40
aliases: ["/classrooms/algorithm-design/lesson/40"]
---
This is a brief introduction to dynamic programming. We showed through examples what we mean by breaking down a problem into sub-problems. There are usually different ways to implement the computations. One would be "bottom-up" where we start from the base cases and compute the values until we reach the desired value. Another would be "top-down" in which we recursively compute the answers for smaller problems, on demand, but try to store the computed valued in order not to compute them multiple times. This technique is usually called "memoization".

Sometimes, especially for "bottom-up" implementations it is possible to store only one part of the computed values at a time and free the memory for other parts once they have served their job in the computations.
