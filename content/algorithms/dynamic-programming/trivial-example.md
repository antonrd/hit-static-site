---
title: "Trivial example"
type: docs
weight: 20
---
Let's start with a very simple example to illustrate the above words. Think about the [Fibonacci numbers](https://en.wikipedia.org/wiki/Fibonacci_number). How do we compute the 100th such number: by taking the sum of the 98th and 99th. This can be considered a very simple example of breaking down a task into smaller tasks. In order to get the answer for the problem with size `N` we need to solve for the problems with sizes `N-1` and `N-2`. If we go down like that we will reach the trivial problems with sizes 1 and 2, which we know the answers for. They come from the very definition of Fibonacci numbers: `F(1) = 1` and `F(2) = 1`. In some cases it may be stated that the first two values are 0 and 1, which is not so important for our example.

This means that if we compute the answers for problems with increasing sizes we will eventually get to the answer for `F(100)`.

Let's see how memoization works for us here. The definition for the Fibonacchi numbers looks like this: `F(n) = F(n-1) + F(n-2)`. If we write a program, which makes recursive calls to get the answer for smaller tasks we may get in trouble very quickly. This is because each new call will spawn two new calls. This means that at the top most level of the recursion there will be one call, at level two there will be two calls, at level 3 - there will be 4 calls and so on. At every next level there will be twice as many calls as the level above it. Of course, at some level the recursion will be reaching one of the trivial cases (`F(1)` and `F(2)`) but for high enough indexes the levels at which we reach the trivial versions of the problem will be very far away from the initial call.

Here is pseudocode for how this solution would look like:

```ruby
def fibonacci(N)
  if N <= 2 return 1;
  return fibonacci(N-1) + fibonacci(N-2)
end
```

As a small homework task you can try to compute the number of recursive function calls that we happen for different values of `N`. This will help you observe the exponential growth of these calls as N increases linearly.

So, this implementation of dynamic programming won't be efficient enough if we want to find Fibonacci numbers with too high indexes, like 100 for example. Why is that? The main reason is that the same Fibonacci number will get computed over and over again. This is because each Fibonacci number, except the first one, is used to compute two other numbers. This is a very common situation in different problems requiring dynamic programming - the same sub-problem is a building block for computing more than one bigger sub-problem. Instead of re-computing the value each time we need it we could store it once and reuse it from memory when we need it. This is what memoization is about.

For Fibonacci numbers let's start computing the answers from the bottom up. Initially we store F(1) and F(2) and them continue with computing for F(3), F(4), F(5) and so on. Pseudocode will look like that:

```ruby
F(1) = 1
F(2) = 1

for i = 3 to N
  F(i) = F(i-1) + F(i-2)
end
```

This way we compute the answer to each sub-problem only once. Of course, we could stick to our initial recursive solution starting from the top and going down. But we need to make sure that we cache the computed values instead of computing them over and over again. Here is some code:

```ruby
F(1) = 1
F(2) = 1

def fibonacci(N)
  if F(N) is not stored
    F(N) = fibonacci(N-1) + fibonacci(N-2)
  end

  return F(N)
end
```

This solution stores the computed values in memory and reuses them if they were already computed. If a value has not yet been computed we make recursive calls to get the answer for the smaller sub-problems. However, since no value is computed more than once the complexity is now linear, instead of the exponential growth of spawned tasks that we observed with the recursive solution not using memoization.
