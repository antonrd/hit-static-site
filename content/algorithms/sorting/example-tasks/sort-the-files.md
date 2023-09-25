---
title: "Sort the files"
type: docs
weight: 10
aliases: ["/classrooms/algorithm-design/lesson/20"]
---
### Task Statement
You know how sometimes files with numbers in them get sorted lexicographically, which produces incorrect sequences of files. For example people use to have tons and tons of pictures and they are often named like that: `IMG123456.jpg`.

Imagine that you have a set of `N` image files, which are numbered from `1` to `N` like that: `IMG1.jpg`, `IMG2.jpg`, `IMG3.jpg`, and so on.

If sorted by name the order could start to look incorrect if there are at least 10 files:

```
IMG1.jpg
IMG10.jpg
IMG11.jpg
IMG12.jpg
…
```

Your task is given `N` to return the sorted lexicographically list of file names. `N` is in the range `[1, 1,000,000]`. In 40% of the test cases `N` will be no higher than `1,000`. If `N` if higher than `1,000` return just the first `1,000` file names.

Write a function which accepts two parameters - the number `N` and a list in which it must store the filenames in the correct sorted order. Look at the boilerplate code for your favorite language.

Here is an example test case:

**SAMPLE INPUT**

```
16
```

**SAMPLE OUTPUT**

```
IMG1.jpg
IMG10.jpg
IMG11.jpg
IMG12.jpg
IMG13.jpg
IMG14.jpg
IMG15.jpg
IMG16.jpg
IMG2.jpg
IMG3.jpg
IMG4.jpg
IMG5.jpg
IMG6.jpg
IMG7.jpg
IMG8.jpg
IMG9.jpg
```

<hr/>

### Solution

Probably the most trivial solution that comes to mind for this task is to generate all the files names, sort them and take the first 1000 (or less if `N < 1000`). However, this solution will require sorting 1,000,000 strings in the worst case. Given the time constraints of the task this may not be a fast enough solution.

An alternative solution would be generate only the filenames that will be returned in the output. To do that we will need to consider the sorting logic for the filenames.

Let's say that we need to output the first `P` files where `P = min(N, 1000)`. The filenames that come first are the ones starting with `IMG1` regardless of the digits that follow. Next come the ones starting with `IMG2`, then with `IMG3` and so on.

Among the filenames starting with `IMG1` the first is `IMG1.jpg`, the rest are sorted according to their second digit and the logic is the same as for ordering all filenames by the first digit. We should follow this logic to generate the filenames in the right order.

A recursive implementation could help us here. We could have a method, which is first called with the prefix `IMG` and it tries consecutively to attach to it 1, 2, 3, etc. Then it calls itself with `IMG1`, `IMG2`, `IMG3`, etc and does the same thing. Of course when the number in the filename is higher than `N` there is not need to continue as we are only interested in filenames with the numbers in the range `[1, N]`. Also, since we generate the filenames in sorted order once we have generated the first `P` filenames, we can stop.

Below is a Ruby implementation of solution that follows this idea:

```ruby
def rec n, level, filename, files
  return if files.count == 1000 || filename > n
  files << filename if level > 0

  (0..9).each do |digit|
    next if digit == 0 && level == 0

    rec n, level+1, filename*10+digit, files
  end
end

files = []

# n is the total number of files
rec(n, 0, 0, files)

puts files.map { |number| "IMG#{number}.jpg" }
```

The time complexity of this solution is `O(P)` because it only generates the first `P` filenames and does no additional work.

For this task's fast solution there was no direct application of a standard sorting algorithm involved, as you can see. It is a demonstration that when we say sorting we don't always mean just applying your favourite sorting algorithm to a set of elements.
