---
title: "Numeric palindromes"
type: docs
weight: 30
---
### Task Statement

A palindrome is а word or a phrase or a number, that when reversed, stays the same.

For example, the following sequences are palindromes : "azobi4amma4iboza" or "anna".

But this time, we are not interested in words but numbers.
A "number palindrome" is a number, that taken backwards, remains the same.

For example, the numbers 1, 4224, 9999, 1221 are number palindromes.

Implement a function, which given an integer computes if it's a palindrome.

### Input

One integer `n`, where `0 < n <= 10,000,000,000`.

### Output

Your function must return a boolean `true` if n is a palindrome and `false` otherwise.

### Test examples

| Input | Output |
|-------|--------|
| 1 | true |
| 42 | false |
| 100001 | true |
| 999 | true |
| 123 | false |

### Solution

There are at least two efficient solutions to this problem. Both offer trade-off between memory used and number of times you traverse the input number. Of course, since we are talking about numbers with no more than 11 digits the additional memory or time spent don't really matter. However, we will look at the two possible ways to solve the problem, to illustrate how often in programming you have to choose between different solutions based on the limitations that you have in your particular case.

One solution using additional memory would store the separate digits of the number in an array and then sequentially compare in the array the digits that must be the same if the number is a palindrome. In order to extract the separate digits of the number into an array you can sequentially divide it by 10, get the remainder and continue with the rest of the number until you get all digits. Then, in the array, compare the first and last digit, the second and last but one, and so on.

The second solution does not use additional memory but it requires two passes over the number. With the first pass you can check the length of the number. This will help you in extracting the digits from the left side of the number. Once you know that the number has `L` digits, this would mean that you can get the left-most digit by dividing the input number `N` by `10 ^ (L-1)`. The while part of this division result will give you the left-most digit. To get the right-most digit just divide by 10 and get the remainder.

This way you can sequentially extract the left-most and right-most digits of the number and compere them. After that strip out these two digits and repeat the process. Do that until you are in the middle of the number. Below are two implementations of these ideas.

You may be wondering which solution it is better to choose at an interview. The approach that we recommend in such situations is to ask your interviewer. Describe briefly the two solutions and what trade-offs they involve. Then most likely the interviewer will either tell you to choose one of the two solutions or will give you some additional constraints that make one of the solutions more favourable.


#### In Python with additional memory


```python
def is_numeric_palindrome(n):
  arr = []
  while(n > 0):
    arr.append(n % 10)
    n = n // 10

  num_len = len(arr)
  for i in range(num_len / 2):
    if arr[i] != arr[num_len - i - 1]:
      return False

  return True
```


#### In Ruby with two passes over the number

```ruby
def is_numeric_palindrome number
  tmp_number = number
  digits_count = 0
  while tmp_number > 0
    tmp_number /= 10
    digits_count += 1
  end

  degree_of_10 = 10 ** (digits_count - 1)

  while number > 0
    left_most_digit = number / degree_of_10
    right_most_digit = number % 10
    return false if left_most_digit != right_most_digit

    # To strip out the left-most and right-most digits, first we get the remainder
    # when dividing by the right degree of 10 and them we get the while part of the
    # result when dividing by 10 to strip out the right-most digit.
    number = (number % degree_of_10) / 10

    # We decrese the degree of 10 by zeroes because we've removed 2 digits from the
    # original number
    degree_of_10 /= 100
  end

  true
end
```
