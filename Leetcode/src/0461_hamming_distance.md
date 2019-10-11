# 461. Hamming Distance

## Description

The Hamming distance between two integers is the number of positions at which the corresponding bits are different.

Given two integers x and y, calculate the Hamming distance.

**Note:**

`0 ≤ x, y < 231.`

**Example:**

```
Input: x = 1, y = 4

Output: 2

Explanation:
1   (0 0 0 1)
4   (0 1 0 0)
       ↑   ↑
```

The above arrows point to positions where the corresponding bits are different.

## Solution

```cpp
class Solution {
public:
    int hammingDistance(int x, int y) {
     return bitset<32>(x^y).count()；
    }
};
```

```cpp
class Solution {
public:
    int hammingDistance(int x, int y) {
        int res = 0;
        while( x != 0 || y != 0 ) { // 当 x 或者 y 有一个不为 0 时       
            if((x&1) != (y&1)) {  // 若低位相等，则结果加1；
                res++;
            }   
            
            x = x >> 1;  // x 向右移一位
            y = y >> 1;  // y 向右移一位
        }
        
        return res;
    }
};
```