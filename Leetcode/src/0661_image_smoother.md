# 661. Image Smoother

[problem link](https://leetcode.com/problems/1-bit-and-2-bit-characters/)

## Description

Given a 2D integer matrix M representing the gray scale of an image, you need to design a smoother to make the gray scale of each cell becomes the average gray scale (rounding down) of all the 8 surrounding cells and itself. If a cell has less than 8 surrounding cells, then use as many as you can.

**Example 1:**

```
Input:
[[1,1,1],
 [1,0,1],
 [1,1,1]]
Output:
[[0, 0, 0],
 [0, 0, 0],
 [0, 0, 0]]
Explanation:
For the point (0,0), (0,2), (2,0), (2,2): floor(3/4) = floor(0.75) = 0
For the point (0,1), (1,0), (1,2), (2,1): floor(5/6) = floor(0.83333333) = 0
For the point (1,1): floor(8/9) = floor(0.88888889) = 0
```

**Note:**

1. The value in the given matrix is in the range of [0, 255].
2. The length and width of the given matrix are in the range of [1, 150].

## Solution

```cpp
class Solution {
public:
    vector<vector<int>> imageSmoother(vector<vector<int>>& M) {
        int rows = M.size();
        int cols = M[0].size();
        int temp = 0;
        vector<vector<int>> result(rows, vector<int>(cols));
        for(int i = 0; i < rows; ++i){
            for(int j = 0; j < cols; ++j){
                result[i][j] = cal(M, i, j) / getSize(M, i, j);
            }
        }
        return result;
        
    }
    
    int get(vector<vector<int>>& M, int i, int j){
        if(i >= 0 && i < M.size() && j >= 0 && j < M[0].size()){
            return M[i][j];
        }
        return 0;
    }
    
    int cal(vector<vector<int>>& M, int i, int j){
        int sum = 0;
        for(int k = i-1; k <= i + 1; ++k)
            for(int kk = j - 1; kk <= j + 1; ++kk)
                sum += get(M,k,kk);
        return sum;
    }
    int getSize(vector<vector<int>>& M, int i, int j){
        int l = max(0, i-1);
        int r = min(int(M.size()-1), i+1);
        int u = max(0, j - 1);
        int d = min(int(M[0].size()-1), j+1);
        return (r - l + 1) * (d - u + 1);
    }
};
```