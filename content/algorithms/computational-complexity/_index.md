---
title: "Computational Complexity"
type: docs
weight: 20
no_list: true
---
As mentioned earlier in the course, we will devote a section to computational complexity because this is a key thing to consider when designing almost any software solution - from a small program to big software systems. Let's begin with some informal explanations of what it is and why it is so important for your tech interviews.

Imagine that you are given a task to generate all palindromes using a set of `N` latin letters. One brute force solution that comes to mind is to generate all permutations of the `N` letters and to check for each one of them if it's a palindrome. Some people could say that the task is easy because this solution is easy to come up with. However, to generate all permutations of the `N` letters you would need to generate `N!` words. For even small values of `N` this becomes a solution, which will not finish in a reasonable amount of time. Because of that we will need to design a better approach, which can compute the answer much faster.

At tech interviews you will have to compute and explain the time and memory complexity of your solutions quite often. This is something that will show your interviewer that you can evaluate if a solution is feasible given the problem requirements. In real life this is also a very useful skill. Actually, in our opinion, it's a must-have skill for good software engineers.

Two resources that are limited for our programs are time and memory. Of course there are others but these two are usually the main constraints to our solutions. That is why in this section we will focus on time and memory complexity. We will talk about why they are things that you should definitely be able to understand and measure at a tech interview. Of course, we will also provide some explanations and examples to help you understand them better.
