---
title: "How to use it in real life?"
type: docs
weight: 40
---
Hopefully by now you have built a good understanding of what computation complexity is about. You should be able to compute the time and memory complexity of most algorithmic solutions that you can face at a programming interview or at work.

Don't worry if things are not very clear now. The best thing to do in order to get more proficient in this is, as usually, to practice. Just take different algorithmic problems and their solutions and try to evaluate the time and memory complexity. Then look at some explanations about them to see if you are getting it right. It will take time but once you have this skill mastered, it will be invaluable to you.

There is one more aspect to computational complexity and how it helps us evaluate different software solutions. Let's say that you can determine the time complexity of a solution. You also know the expected inputs. How do you decide if the solution will run fast enough?

If the time complexity of a solution is `O(N^2)` and `N` can be as big as `10,000`, is that good or not?

First of all, it depends on the time constraints that you are under. Secondly, you need to consider the machine(s) where the solution will run. With time you will start to build better intuition about how quick a solution will really be given it's time complexity and the input size. This won't happen immediately, it takes practice, but for sure, you'll get better at this as you work through various examples.

However, knowing the time or memory complexity of different solutions to the same problem also gives you the ability to compare them and decide which one is better, or what trade-offs are required.

With memory it's probably somewhat easier to evaluate and still it depends. For example the programming language maybe not allow you to compute the exact memory used. If you implement stuff in C it will probably be easier to know exactly how much memory will be used. If you use languages offering higher level abstractions like C++ (with STL for example) or Ruby, Java, Python, you may need to experiment to see how much memory is consumed.

And still if you know the memory complexity, you will be able to have a pretty good expectation about the memory used. This is much better than nothing.

Now with this knowledge under the belt you can continue to the next sections, which cover specific algorithmic topics, but before that we have one last small lesson related to this topic.
