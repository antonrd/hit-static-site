---
title: "Count number's factors"
type: docs
weight: 20
aliases: ["/classrooms/algorithm-design/lesson/25"]
---
### Task Statement

This is a classic task requiring you to count all integer factors of a positive integer number `N`, including 1 and the number itself. Note that this is not just about the prime factors but all of them.

For example for 12 there are 6 such factors: 1, 2, 3, 4, 6, 12.

In this task `N` will be in the range `[1, 10^12]`.

Your function will receive one argument - the number `N`. It must return one integer - the number of all factors of `N` as described above.

Here is an example test case:

**SAMPLE INPUT**

```
12
```

**SAMPLE OUTPUT**

```
6
```

<hr/>

### Solution

All integer factors of a given integer `N` are the product of some subset of the prime factors of `N`. One could think that if we just count all subsets of the prime factors of `N` we would get the answer. However, this won't give you the correct answer in many cases. The reason is that if `N` has several prime factors that are equal it doesn't matter, which of them are used when forming the subsets. Here is an example with `N=12`, `12 = 2 * 2 * 3`. Its factors are `1, 2, 3, 4, 6, 12`. All subsets of the prime factors are `2^3 = 8` but 12 only has 6 different factors. This is because it has 2 as a factor twice. So, we need something smarter to compute the answer.

If we think about it we can group the prime factors by value. For 12 we would have 2 groups: 2 times the factor 2 and 1 time the factor 3. To form a factor of `N` we would need to choose from each group the number of factors to use: from 0 up to the number of factors in the group. Once we have chosen how many factors to use from each group we multiple them and this produces a factor of `N`. This would mean that if `Gi` is the number of factors in the i-th group there will be `(G1 + 1) * (G2 + 1) * ... * (Gk + 1)` different ways to choose factors from the groups.

This product gives us the desired count of all integer factors of `N`.

Now we need to find an efficient way to find all prime factors of `N` and we are done with this problem. Finding the prime factors is a classic problem, one that you should definitely be confident solving at an interview.

An approach that may come to mind first is to iterate over positive integers starting at 2 until we reach `N`. For each number we check if it divides `N` and if the number is prime. If both conditions are met it is a prime factor of `N`. To check if a number `P` is prime we could check if any number between 2 and the squared root of `P` divides it. If there is none such number then `P` is prime. This approach could work fast enough in some situations but there are two problems: 1) we will iterate over all numbers between 1 and `N` and 2) for all factors of `N` we will run another `O(sqrt(P))` steps to check if the number is prime. For our task's constraints this will be too slow for some test cases.

One quick optimization is not to iterate all numbers between 1 and `N` but to only try the numbers between 1 and the squared root of `N`. Each time we find a prime factor we divide `N` by it as many times as needed. In the end the remaining value will either be 1, or something bigger than 1. If it's bigger than 1, this means that `N` has a prime factor, which is bigger than the squared root of `N`.

The second efficiency problem described above can be resolved by using a technique called "the sieve of Eratosthenes". It allows us to find the prime numbers in a given range more quickly then just checking for each number if it's prime or not.

The idea is that we maintain in memory an array `P`, for which `P[i]` tells us if `i` is primer or not. In the beginning we set all values of `P` to `true`. Then we start to iterate from 2 up to the other end of the range to cover. For each number `i` we iterate we check if `P[i]` is currently marked as prime. If it is we run a nested loop starting from `i * i` with a step of `i` and mark the values that we iterate as not primer because obviously `i` is a factor for them.

Once we reach the end of the array `P` it will have correct values indicating, which numbers are prime. You can read a lot more about this algorithm on the Internet. There is plenty of explanation and analysis done.

Let's apply this idea to the solution described above. We already said that we will only iterate between 1 and the squared root of `N`. We can iterate over these numbers and apply the sieve of Eratosthenes at the same time. This way, once we reach a number we will have in `P` information about whether it is prime or not. This will speed up the solution compared to the version in which we check for each factor if it's primer or not. Below is a solution in Ruby:

```ruby
# n is the input integer for the task
limit = Math.sqrt(n).to_i

is_prime = [true] * limit

i = 2
ans = 1

while i <= limit
  if is_prime[i]
    cnt = 0
    while n % i == 0
      n /= i
      cnt += 1
    end

    ans *= (cnt + 1)

    j = i*i
    while j <= limit
      is_prime[j] = false
      j += i
    end
  end

  i += 1
end

ans *= 2 if n > 1

puts ans
```
