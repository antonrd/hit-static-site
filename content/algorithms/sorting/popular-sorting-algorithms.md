---
title: "Popular sorting algorithms"
type: docs
weight: 20
aliases: ["/classrooms/algorithm-design/lesson/41"]
---
You are probably already familiar with different techniques for sorting elements. It is not impossible that sometimes at an interview you would just need to write code, which orders a set of elements by some value. For such cases it is always good to be able to quickly implement something from scratch. Probably the simplest and easiest to write sorting algorithms are "selection sort" and "bubble sort". Both algorithms have time complexity `O(N^2)`, where `N` is the number of elements to sort. We will not go in details about how these algorithms operate because there are plenty of excellent resources out there covering this. The Wikipedia article on sorting linked at the bottom of this lesson is a good start. It tells you about some other interesting algorithms as well.

There are some other more efficient algorithms in terms of their speed. Quick sort, merge sort and heap sort are probably the most famous ones.

One interesting aspect of these algorithms is their running time for different inputs. For example it's worth mentioning that *selection sort* performs `O(N^2)` operations regardless of the input. However, *bubble sort* could be very quick if given input that is already sorted and it will take `O(N^2)` if the output is sorted in reverse for example. That may be an important feature in some situations. It's worth considering such differences between seemingly similar algorithms. Sometimes interviewers may be curious to test your knowledge in this regard.

Another such example is *quick sort*, which depending on the implementation could perform `O(N^2)` operations in the worst case. At the same time *heap sort* and *merge sort* always have time complexity `O(N*logN)` regardless of the input.

### Resources

- Wikipedia <a href="https://en.wikipedia.org/wiki/Sorting_algorithm" target="_blank" rel="noopener noreferrer">Sorting algorithms article</a>
- TopCoder <a href="https://www.topcoder.com/thrive/articles/Sorting/" target="_blank" rel="noopener noreferrer">tutorial on sorting</a>
