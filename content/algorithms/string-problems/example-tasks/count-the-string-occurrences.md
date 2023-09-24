---
title: "Count the string occurrences"
type: docs
weight: 10
---
### Task Statement

You are given two strings T and P. Write a program, which counts how many times P is found in T. If different occurrences of P in T overlap count each one of them.

Here is an example:

T = babalabalabalatheend
P = alabala

The string P is found twice in T, first occurrence starts at position 4 (first letter is at position 1) and the second occurrence start at position 8.

Both strings will contain only lower-case latin letters (‘a’-’z’) and will have at least one letter. The maximum possible length for T is 100,000 and for P - 10,000.

The input is read from the standard input. The first line contains the string T and the second line contains the string P. The strings T and P will be such so that P does not occur in T more than 100 times. Try to think of a solution, which takes advantage of this.

The output is written to the standard output. It must contain only one integer number - the number of occurrences of P in T as described above.

**SAMPLE INPUT**

```
babalabalabalatheend
alabala
```

**SAMPLE OUTPUT**

```
2
```

<hr/>

### Discussion
This task was partially covered in the overview lesson of this section. It's a classic version of the task for string pattern matching. In this particular task the constraints for the maximum lengths of `T` and `P` are such that the most straight forward algorithm is not supposed to score the maximum points. However, it will pass some of the test cases. The *Rabin-Karp algorithm*, mentioned in the overview, will do a better job but it will probably not be enough for the hardest test cases.

This is a great opportunity to try implementing the *Knuth-Morris-Pratt algorithm*, which should be efficient enough to pass all test cases.
