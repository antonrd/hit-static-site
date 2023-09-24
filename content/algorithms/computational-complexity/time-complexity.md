---
title: "Time complexity"
type: docs
weight: 20
---
Let's look at some examples in order to get a better understanding of time complexity of an algorithm. Later we will also look at memory complexity as this is another limited resource that we have to deal with.

First of all, time complexity will be measured in terms of the input size. As you saw in the palindrome example from last lesson, `N` was the number of latin letters to use for building palindromes. We said that all permutations of these `N` letters are `N!`. So to generate them we would perform a number of steps that is proportional to `N!`. Of course, it is also important how many steps it takes to generate each separate permutation. It is possible to do that with a constant amount of steps. We will not go into details how this can be done but trust us.

This means that the number of steps to generate each next permutation does not depend on the size of the input. For each generated permutation we would need to check if it is a palindrome. One way to do it is to compare the first and last letters, then the second and the last but one and so on. This will require a number of steps that is proportional to the number of letters - `N`. So, for each permutation we will perform that many steps.

With all that in mind we will have to perform a number of steps that is proportional to `N * N!` in order to execute our brute force solution. This number will be multiplied by some constant but usually when this constant is not too high we don't take it into account. Now that we have quickly analysed the number of steps required, we can clearly see that the number of steps will grow very quickly with increasing values of `N`. If your interviewer tells you, for example, that `N` can be as high as 100, then there is no use in even considering such a solution. 100! is a tremendously large number and a solution with this time complexity is not practical. Of course, it is a possible initial solution to mention at the interview, but you need to acknowledge that you need something better and that this is just a starting point. Being able to describe to the interviewer why such a solution is not feasible is also a useful skill.

Let's look at another example. Imagine a block of code, which sorts an array of integers:

```cpp
// An array `arr` with `len` integers in it is sorted.
for (int i = 0; i < len - 1; i++) {
  for (int j = i + 1; j < len; j++) {
    if (arr[i] > arr[j]) {
      int tmp = arr[i];
      arr[i] = arr[j];
      arr[j] = tmp;
    }
  }
}
```

This algorithm has two nested loops. The outer one goes through the numbers from left to right and finds the number that must be in each position. For the number at position 0 it finds the minimum of all numbers. Then, for the number at position 1 it finds the minimum of all remaining numbers and so on. The question we will answer here is: what is the time complexity of this algorithm?

The outer loop will perform `N-1` iterations where `N` is the number of the numbers to sort. This is our parameter indicating the size of the input. For each iteration of the outer loop the inner loop will perform a different number of steps. In the first interation it will perform `N-1` steps, next it will perform `N-2` steps and so on.

Inside the loops there is a comparison and in some cases there will be three operations used for swapping two values. These operations inside the loops take constant time regardless of `N`. That is why we will be more interested in computing the total number of interations that the two loops will perform. To compute that we just need to sum up the number of iterations of the inner loop: `(N-1) + (N-2) + ... + 2 + 1 = N * (N-1) / 2`. This is a number proportional to `N^2` because if we expand it we will get `N^2 / 2 - N / 2`. We are always interested in the term with the highest degree and here this is `N^2`. It is multiplied by a constant - 1/2 - but this does not change the fact that the total number of steps will be proportional to `N^2` and as `N` grows linearly our algorithm's speed will slow down quadratically.

Another important thing to mention is that you are usually interested in finding out the slowest part of your algorithm. Maybe for some task you have a solution that does some preprocessing first taking roughly `N*M` steps, with `N` and `M` being some values identifying the size of your input. But then if your core algorithm performs `N*M^2` steps to run, then you can say that this is your actual time complexity because it is of higher order than `N*M`.

There are several formal definitions for how we define computational complexity and they can be used depending on the case. For most tech interviews and real-time examples you will need to use the so called big-O notation. Below we have included links to a few useful resources that will tell you more about big-O and other notations using more or less formal language.

## Resources
- <a href="https://www.topcoder.com/community/data-science/data-science-tutorials/computational-complexity-section-1/" target="_blank" rel="noopener noreferrer">TopCoder's 2-part tutorial</a> on computational complexity is a good place to start, it also covers several notations. From the first part the whole article is useful. You can perhaps skip the section “Finally, formal definitions” if you wish. From the second part, everything up to the section “The substitution method” is worth covering for the purpose of interviews. The rest is more or less optional.
- <a href="http://www.cprogramming.com/tutorial/computersciencetheory/algorithmicefficiency1.html" target="_blank" rel="noopener noreferrer">This tutorial from Cprogramming.com</a> describes the matter in an easy to understand way
- And <a href="https://rob-bell.net/2009/06/a-beginners-guide-to-big-o-notation/" target="_blank" rel="noopener noreferrer">this article</a> uses a lot of examples to give you a better intuition
- From MIT we have <a href="http://web.mit.edu/16.070/www/lecture/big_o.pdf" target="_blank" rel="noopener noreferrer">a great lecture handout</a>, which has some formal definitions but also has some good examples
- <a href="https://www.educative.io/collection/page/5307417243942912/5630721452408832/5740423507083264" target="_blank" rel="noopener noreferrer">This course on Big-O</a> from Educative is quite comprehensive (Paid)
