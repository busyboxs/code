# 556. Next Greater Element III

## Description

Given a positive `32-bit` integer `n`, you need to find the smallest `32-bit` integer which has exactly the same digits existing in the integer n and is greater in value than n. If no such positive `32-bit` integer exists, you need to return -1.

**Example 1:**

```
Input: 12
Output: 21
```

**Example 2:**

```
Input: 21
Output: -1
```

## Solution

```cpp
class Solution {
    
private:
    bool nextPermutation(string& nums) {
        if(nums.empty())
            return false;
        int i = nums.size() - 1;
        
        while(i >= 1 && nums[i] <= nums[i-1])
            i--;
        
        if(i == 0)
            return false;
        
        int j = nums.size() - 1;
        
        while(nums[j] <= nums[i-1])
            j--;
        swap(nums[i-1], nums[j]);
        reverse(nums.begin()+i, nums.end());
        return true;
    }
    
public:
    int nextGreaterElement(int n) {
        string nums = to_string(n);
        if(!nextPermutation(nums))
            return -1;
        long long result = stoll(nums);
        
        return (result > INT_MAX || result <= n) ? -1: result;
    }
};
```