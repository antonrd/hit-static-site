---
title: "Jump over numbers"
type: docs
weight: 10
---
### Task Statement

You are given a list of non-negative integers and you start at the left-most integer in this list. After that you need to perform the following step:

* Given that the number at the position where you are now is `P` you need to jump `P` positions to the right in the list. For example, if you are at position 6 and the number at position 6 has the value 3, you need to jump to position 6 + 3 = 9. Repeat this operation until you reach beyond the right-side border of the list.

Your program must return the number of jumps that it needs to perform following this logic. Note that the list may contain the number 0, which mean that you can get stuck at a this position forever. In such cases you must return the number -1.

The length `N` of the input list will be in the range [1, 1000].


**SAMPLE INPUT**

```
3 4 1 2 5 6 9 0 1 2 3 1
```

**SAMPLE OUTPUT**

```
4
```

**Note:** In the sample example you start at position 1, where the number is 3. Then you must jump to position 4, where the number is 2. After that you jump to position 6 where the number is 6. This will lead you to position 12, which is the last number in the list and has the value 1. From there you jump 1 position to the right and must stop. This is a total of 4 jumps.

### Solution

This is a simple task, which involves running a loop that iterates over the indexes of the input list or array in the order that is dictated by the input data.

You must start at the left-most position, which usually in programming languages is with index 0. Then you can have a loop, which iterates over the array by computing the next index to visit based on the value contained in the current index.

Below you will find example solutions in several programming languages.

**C++**

```cpp
#include <vector>

using namespace std;

int jump_over_numbers(const vector<int>& list) {
    int pos = 0;
    int ans = 0;
    while (pos < list.size()) {
        int curr_val = list[pos];
        if (curr_val == 0) {
            return -1;
        }
        ans++;
        pos += curr_val;
    }

    return ans;
}
```

**Java**

```java
import java.util.List;

class Solution {
  public static int jump_over_numbers(List<Integer> list) {
    int pos = 0;
    int ans = 0;

    while (pos < list.size()) {
      if (list.get(pos) == 0) {
        return -1;
      }
      ans++;
      pos += list.get(pos);
    }

    return ans;
  }
}
```

**Python**

```python
def jump_over_numbers(list):
    pos = 0
    ans = 0
    while pos < len(list):
        if list[pos] == 0:
            return -1
        ans += 1
        pos += list[pos]

    return ans
```

**Ruby**

```ruby
def jump_over_numbers(list)
  pos = 0
  ans = 0
  while pos < list.count
    return -1 if list[pos] == 0
    ans += 1
    pos += list[pos]
  end

  ans
end
```
