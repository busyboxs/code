# 628. Maximum Product of Three Numbers

[problem link](https://leetcode.com/problems/maximum-product-of-three-numbers/)

## Description

Given an integer array, find three numbers whose product is maximum and output the maximum product.

**Example 1:**

```
Input: [1,2,3]
Output: 6
```

**Example 2:**

```
Input: [1,2,3,4]
Output: 24
```

**Note:**

1. The length of the given array will be in range [3,10^4] and all elements are in the range [-1000, 1000].
2. Multiplication of any three numbers in the input won't exceed the range of 32-bit signed integer.

## Solution

```cpp
class Solution {
public:
    int maximumProduct(vector<int>& nums) {
        int max1 = INT_MIN;
        int max2 = INT_MIN;
        int max3 = INT_MIN;
        int min1 = INT_MAX;
        int min2 = INT_MAX;
        
        for (auto num: nums) {
            if(num > max1) {
                max3 = max2;
                max2 = max1;
                max1 = num;
            }else if(num > max2) {
                max3 = max2;
                max2 = num;
            }else if(num > max3){
                max3 = num;
            }
            
            if(num < min1) {
                min2 = min1;
                min1 = num;
            }else if(num < min2){
                min2 = num;
            }
        }
        
        return max(min1*min2, max2*max3)*max1;
        
    }
};
```