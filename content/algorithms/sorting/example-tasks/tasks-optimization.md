---
title: "Tasks optimization"
type: docs
weight: 20
aliases: ["/classrooms/algorithm-design/lesson/21"]
---
### Task Statement

A worker has a set of `N` tasks to complete. For each task the worker knows the time in minutes it will take to complete. This is dependent on the difficulty of the task. So, a task with difficulty `D` takes `D` minutes to complete. The worker has a limited amount of time T during which he wants to complete as many tasks as possible.

As mentioned above the tasks have different difficulty and when switching from one task to another with difficulties `D1` and `D2`, the worker needs `|D1 - D2|` minutes to prepare for working on the next task.

The number of tasks `N` is in the range `[1, 10,000]`. The total time T is in the range `[0, 200,000,000]`. The task difficulties are integer numbers in the range `[1, 10,000]`.

You need to write a function, which computes the maximum number of tasks that can be completed within the given time `T`. The function accepts as arguments the number `N` and `T` and a list of the task difficulties. It must return one integer - the maximum number of tasks that can be completed within the given time limit.

Here is an example test case.

**SAMPLE INPUT**

```
5 65
24 23 22 10 20
```

**SAMPLE OUTPUT**

```
3
```


All five tasks cannot be completed within the allowed 65 minutes, but it is possible to accomplish three tasks, for example tasks 4, 5, 3 if completed in this order.

<hr/>

### Solution

This task is a great example of a task that requires you to use sorting but the way it is implemented is not the important part. It is more about useful features that sorting gives us.

In order to understand how to use sorting in this task first we need to make a few interesting observations.

To find the best answer for a given input we would need to choose the tasks to complete and the order in which to complete them. The tasks themselves take time based on their difficulty and the order of execution affects the cost of switching between consecutive tasks.

The first important observation is the of we have chosen to complete a set of tasks `T = {T1, T2, ... , Tn}` the best order to choose is in increasing or decreasing difficulty. Why is that? Let's say that the least difficult task in the set is `Tp` and the most difficult task is `Tq`. If we execute the tasks in increasing order of difficulty the total sum of switching costs will be equal to `Tq - Tp`. You can check that yourselves. Could we do better than that? In any other ordering in which the tasks between `Tp` and `Tq` are not in increasing difficulty the sum of switching costs will be higher than `Tq - Tp` because we will be switching between tasks with higher and lower difficulties, moving up and down instead of just going up.

The second important observation is that if we choose a set of tasks to complete `T = {T1, T2, ... , Tn}`, if they don't come immediately one after the other in the sorted order it is possible to choose some of the tasks in between and come up with a better overall cost.

We already showed that the tasks will be executed in order of increasing difficulty. But let's say that some of the tasks not considered for completion come in between the tasks of the set T when order by increasing difficulty: `T1, Q1, T2, T3, Q2, ... , Qm, Tn`.

If we took instead the first `n` tasks starting at `T1` rather than taking the tasks in the set `T` we would end up with tasks that have lower total difficulty and also the total switching cost when executed in the right order will be lower because the most difficult task won't be `Tn` anymore but some task that has a lower difficulty.

With these two observations in mind we can say that the best solution will consist of a set of tasks that come immediately one after the other when sorted in increasing order of difficulty. The same can be said for decreasing order of difficulty, of course.

Having this in mind, we should sort the tasks by difficulty and obtain the sorted task sequence `S`. Then we try to compute the longest sequence of tasks that can be completed within the given time `T`, starting at each of the given tasks. Then we take the longest sequence found. This solution would have time complexity `O(N^2)` because in the worst case for each possible starting task we would look at a number of other tasks. Of course, we also have to take into account the time complexity of sorting the tasks. If we use an efficient algorithm this should take `O(NlogN)`.

However, we could optimise this by reusing some of the information already computed. Let's say we have sorted the tasks in increasing order of difficulty, the sorted sequence `S`. We start from the first, least difficult task in `S` and continue to add tasks to our set until we reach the time limit `T`. This will be the best possible sequence of tasks starting with the first task in `S`. Then, if we want to try finding the answer when we start at the second element of `S`, we should consider that its best sequence will not end before the end of the best sequence that we found for the first task in `S`.

Since we know the total cost that we found when starting from the first task, we can subtract from it the cost of completing the first task and the cost of switching between tasks 1 and 2. From there we can try to add more tasks on the right side of our sequence. Once we have the best answer when starting at the second tasks in `S` we can apply the same idea starting from the third task in `S`. We continue to do that starting at each task in `S` or until the right side of the sequences that we build reaches the last, most difficult, task in `S`.

The time complexity of the part finding the best answer is linear because we move the left boundary of the sequence only from left to right and the same happens to the right boundary. Since we still need to sort the tasks beforehand the total time complexity of the algorithm will be `O(NlogN)`.

Below is code in Ruby showing this idea. It also precomputes the sums of difficulties for the first one task, then for the first two tasks, and so on. This allows it to quickly compute the total cost for completing the tasks in some arbitrary range. It takes advantage of the fact that for a given subsequence of consecutive tasks within the sorted sequence the total cost is equal to the sum of difficulties of the tasks plus the difference in difficulties between the least difficult and most difficult tasks. More formally, for `T = {T1, T2, ..., Tn}` the cost of completing the subsequence `Ti, Ti+1, ..., Tj-1, Tj` is equal to:

```
sum(Ti, Ti+1, ..., Tj-1, Tj) + Tj - Ti
```

This step is just for convenience. The solution could be implemented without it but we wanted to show you this approach, which could increase the efficiency in some other tasks.

```ruby
# n and t are the values from the task statement
# diffs contain the difficulties of tasks as provided in the input

diffs.sort!

sums = []

sums << 0
diffs.each do |diff|
  sums << sums[-1] + diff
end

ans = 0
last_right = 0

(0..n-1).each do |i|
  while last_right < n && diffs[last_right] - diffs[i] + sums[last_right+1] - sums[i] <= t
    last_right += 1
  end

  ans = [ans, last_right - i].max

  break if last_right == n
end

puts ans
```
