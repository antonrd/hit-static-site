---
title: "Fraction simplification"
type: docs
weight: 10
aliases: ["/classrooms/algorithm-design/lesson/24"]
---
### Task Statement

An operation very often performed on fractions is simplification to lowest terms. If a fraction has numerator N and denominator D, then it is simple if N and D don’t have any common divisors other than 1. Otherwise, the fraction can be simplified to “lower terms” meaning that there is another fraction with the same value where the numerator and denominator are smaller numbers than N and D.

Here are a few examples:

The fraction 3/7 cannot be simplified because 3 and 7 don’t have any common divisors other than 1. The fraction 8/24 on the other hand, can be simplified to 1/3.

Write a function, which given two integers - the numerator and denominator of a fraction returns the simplified fraction, possibly the same one as in the input. To return the result the function will receive a third parameter - a list of two elements in which you need to store the resulting numerator and denominator in this order. In all programming languages the list supplied will have two elements allocated that you need to fill with values.

The integers N and D will be in the range [1, 1,000,000,000].

Here is a sample test case:

**SAMPLE INPUT**

```
77 22
```

**SAMPLE OUTPUT**

```
7 2
```

<hr/>

### Solution

To simplify a fraction one needs to find the greatest integer, which divides both the numerator `N` and the denominator `D` of the fraction. Once this integer is known the `N` and `D` can be divided by it and the resulting numbers will represent the simple fraction that we are looking for in the task. It will be simple because the numerator and the denominator of the new fraction won't have common divisors besides the number 1.

How do we find the greatest common divisor of two integers. That's a very standard task. A naive approach would be to try all numbers starting from `min(N,D)` and going down until we reach a common divisor. However, in this task `N` and `D` can be in the range [1, 1,000,000,000]. The algorithm described above will be linear in terms of the smaller of the two numbers in the worst case and this could be too slow for the given constraints.

There is a much more effective algorithm, which is known as Euclidean algorithm. It starts with the two numbers to find GCD for, let's calls them `A` and `B`. At the first step it represents `A` in terms of `B` plus a reminder `R1`. At the next step it will continue doing the same but the two numbers will now be `B` and `R1`. This continue until the remainder at some step is 0. The last non-zero remainder is the GCD of `A` and `B`. The code would look like that in C++:

```cpp
int gcd(int a, int b) {
  while (b > 0) {
    int temp = b;
    b = a % b;
    a = temp;
  }

  return a;
}
```

More can be read about the algorithm in this [Wikipedia article](https://en.wikipedia.org/wiki/Euclidean_algorithm).
