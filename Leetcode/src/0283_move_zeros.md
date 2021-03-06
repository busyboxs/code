# 283. Move Zeroes

## Description

Given an array `nums`, write a function to move all `0`'s to the end of it while maintaining the relative order of the non-zero elements.

**Example:**

```
Input: [0,1,0,3,12]
Output: [1,3,12,0,0]
```

**Note:**

1. You must do this in-place without making a copy of the array.
2. Minimize the total number of operations.

## Solution

```cpp
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        int i = 0;
        for(int j = 0; j < nums.size(); ++j) {
            if(nums[j] != 0) {
                nums[i++] = nums[j];
            }
        }
        
        while(i < nums.size()) {
            nums[i++] = 0;
        }
        
    }
};
```