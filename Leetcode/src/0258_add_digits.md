# 258. Add Digits

## Description

Given a non-negative integer num, repeatedly add all its digits until the result has only one digit.

**Example:**

```
Input: 38
Output: 2 
Explanation: The process is like: 3 + 8 = 11, 1 + 1 = 2. 
             Since 2 has only one digit, return it.
```

**Follow up:**

- Could you do it without any loop/recursion in O(1) runtime?

## Solution

```cpp
class Solution {
public:
    int addDigits(int num) {
        // https://en.wikipedia.org/wiki/Digital_root
        return 1 + (num - 1) % 9;
    }
};
```