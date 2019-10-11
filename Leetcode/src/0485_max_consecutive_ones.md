# 485. Max Consecutive Ones

## Description

Given a binary array, find the maximum number of consecutive 1s in this array.

**Example 1:**

```
Input: [1,1,0,1,1,1]
Output: 3
Explanation: The first two digits or the last three digits are consecutive 1s.
    The maximum number of consecutive 1s is 3.
```

**Note:**

1. The input array will only contain `0` and `1`.
2. The length of input array is a positive integer and will not exceed 10,000

## Solution

```cpp
class Solution {
public:
    int findMaxConsecutiveOnes(vector<int>& nums) {
        int result = 0;
        int count = 0;
        for(auto num: nums){
            if(num == 1){
                count++;
                result = max(count, result);
            }else{
                count = 0;
            }
        }
        return result;
    }
};
```