# 53. Maximum Subarray

## Description

Given an integer array `nums`, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.

**Example:**

```
Input: [-2,1,-3,4,-1,2,1,-5,4],
Output: 6
Explanation: [4,-1,2,1] has the largest sum = 6.
```

**Follow up:**

If you have figured out the O(n) solution, try coding another solution using the divide and conquer approach, which is more subtle.

## Solution

```cpp
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int sum = 0;
        int max_sum = 0;
        int max_num = nums[0];
        for(int i = 0; i < nums.size(); ++i){
            sum = max(0, sum + nums[i]);
            max_sum =max(max_sum, sum); 
            max_num = max(max_num, nums[i]);
        }
        if(max_num < 0)
            return max_num;
        return max(max_sum, sum);
    }
};
```