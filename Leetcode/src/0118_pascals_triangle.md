# 118. Pascal's Triangle

[problem link](https://leetcode.com/problems/pascals-triangle/)

## Description

Given a non-negative integer numRows, generate the first numRows of Pascal's triangle.

![](../images/PascalTriangleAnimated2.gif)

In Pascal's triangle, each number is the sum of the two numbers directly above it.

**Example:**

```
Input: 5
Output:
[
     [1],
    [1,1],
   [1,2,1],
  [1,3,3,1],
 [1,4,6,4,1]
]
```

## Solution

```cpp
class Solution {
public:
    vector<vector<int>> generate(int numRows) {
        vector<vector<int>> result;
        for(int i = 0; i < numRows; ++i){
            result.push_back(vector<int> (i+1, 1));
            for(int j = 1; j < i; ++j){
                result[i][j] = result[i-1][j-1] + result[i-1][j];  
            }
        }
        return result;
    }
};
```