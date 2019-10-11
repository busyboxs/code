# 349. Intersection of Two Arrays

## Description

Given two arrays, write a function to compute their intersection.

**Example 1:**

```
Input: nums1 = [1,2,2,1], nums2 = [2,2]
Output: [2]
```

**Example 2:**

```
Input: nums1 = [4,9,5], nums2 = [9,4,9,8,4]
Output: [9,4]
```

**Note:**

- Each element in the result must be unique.
- The result can be in any order.

## Solution

```cpp
class Solution {
public:
    vector<int> intersection(vector<int>& nums1, vector<int>& nums2) {
        unordered_set<int> s(nums1.begin(), nums1.end());
        vector<int> res;
        
        for(int i = 0; i < nums2.size(); ++i) {
            if(s.erase(nums2[i]))
                res.push_back(nums2[i]);
        }
        
        return res;
    }
};
```