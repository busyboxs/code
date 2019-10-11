# 167. Two Sum II - Input array is sorted

[problem link](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/)

## Description

Given an array of integers that is already sorted in ascending order, find two numbers such that they add up to a specific target number.

The function twoSum should return indices of the two numbers such that they add up to the target, where index1 must be less than index2.

**Note:**

* Your returned answers (both index1 and index2) are not zero-based.
* You may assume that each input would have exactly one solution and you may not use the same element twice.

**Example:**

```
Input: numbers = [2,7,11,15], target = 9
Output: [1,2]
Explanation: The sum of 2 and 7 is 9. Therefore index1 = 1, index2 = 2.
```

## Solution

```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& numbers, int target) {
        int l = 0;
        int r = numbers.size() - 1;
        while(l < r){
            if(numbers[l] + numbers[r] == target){
                return {l+1, r+1};
            }else if(numbers[l] + numbers[r] > target){
                r--;
            }
            else
                l++;
        }  
    }
};
```