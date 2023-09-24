---
title: "Digit sum"
type: docs
weight: 20
---
### Task Statement

Implement a program, which given an integer ```n```, computes the sum of its digits.

If a negative number is given, the function should work as if it was positive.

For example, if n is ```1325132435356```, the digit's sum is 43.
If n is -10, the sum is 1 + 0 = 1.

In the test cases for this task we will have that `-2^63 < n < 2^63`.

### Test examples

| Input | Output |
|--------|----------|
| 10 | 1 |
| 2 | 2 |
| -3456 | 18 |
| 1325132435356 | 43|


### Solution

This is classic task for separating a number into digits. The usual approach for doing this is to sequentially divide the number modulo 10, which returns the last digit. After that the number is divided by 10 and the whole part is only used. This gives us the number without the last digit.

If you do that to get all digits and sum over them, you will get the answer required in this task.

Here is a sample solution in C++:

```cpp
int digit_sum(long long number) {
  int sum = 0;
  if (number < 0) {
    number *= -1;
  }

  while (number > 0) {
    sum += number % 10;
    number /= 10;
  }

  return sum;
}
```
