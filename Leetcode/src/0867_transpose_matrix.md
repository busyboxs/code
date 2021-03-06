# 867. Transpose Matrix

## Description

Given a matrix `A`, return the transpose of `A`.

The transpose of a matrix is the matrix flipped over it's main diagonal, switching the row and column indices of the matrix.

 

**Example 1:**

```
Input: [[1,2,3],[4,5,6],[7,8,9]]
Output: [[1,4,7],[2,5,8],[3,6,9]]
```

**Example 2:**

```
Input: [[1,2,3],[4,5,6]]
Output: [[1,4],[2,5],[3,6]]
```

**Note:**

1. `1 <= A.length <= 1000`
2. `1 <= A[0].length <= 1000`

## Solution

```cpp
class Solution {
public:
    vector<vector<int>> transpose(vector<vector<int>>& A) {
        int row = A.size();
        int col = A[0].size();
        
        vector<vector<int>> A_trans(col, vector<int>(row, 0));
        
        for(int i = 0; i < row * col; ++i) {
            A_trans[i%col][i/col] = A[i/col][i%col];
        }
        
        return A_trans;
        
        
    }
};
```