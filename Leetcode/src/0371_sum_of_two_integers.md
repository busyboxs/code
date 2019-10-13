# 371. Sum of Two Integers

## Description

Calculate the sum of two integers a and b, but you are not allowed to use the operator + and -.

**Example 1:**

```
Input: a = 1, b = 2
Output: 3
```

**Example 2:**

```
Input: a = -2, b = 3
Output: 1
```

## Solution

```cpp
class Solution {
public:
    int getSum(int a, int b) {
        int res = a;
        // if we don't care carry, and add two sum a and b in bit, we will get
        // 0 + 0 = 0; 0 + 1 = 1; 1 + 0 = 1; 1 + 1 = 0; that is the same result of ^.
        // if we only care carry, and add a and b in bit, we will get 
        // 0 + 0 = 00; 0 + 1 = 00; 1 + 0 = 00; 1 + 1 = 10; that is (a&b)<<1.
        // then we should loop until b is 0, and a is result of a + b.
        while(b != 0) {
            res = a ^ b;  // add a and b without care carry,  
            b = (a & b & 0xffffffff) << 1;  // add a and b only care carry
            a =  res;  // loop add sum(without carry) and carry
        }
        
        return res;
    }
};
```

```cpp
class Solution {
public:
    int getSum(int a, int b) {
        return b == 0? a : getSum(a ^ b, (a&b&0xffffffff)<<1);
    }
};
```