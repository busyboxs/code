# 63. Unique Paths II

## Description

A robot is located at the top-left corner of a *m x n* grid (marked 'Start' in the diagram below).

The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).

Now consider if some obstacles are added to the grids. How many unique paths would there be?

<center>

![](../images/63.png)
An obstacle and empty space is marked as 1 and 0 respectively in the grid.
</center>

Note: *m* and *n* will be at most 100.

**Example 1:**

```
Input:
[
  [0,0,0],
  [0,1,0],
  [0,0,0]
]
Output: 2
Explanation:
There is one obstacle in the middle of the 3x3 grid above.
There are two ways to reach the bottom-right corner:
1. Right -> Right -> Down -> Down
2. Down -> Down -> Right -> Right
```

## Solution

Algorithm

* If the first cell i.e. `obstacleGrid[0,0] = 1`, this means there is an obstacle in the first cell. Hence the robot won't be able to make any move and we would return the number of ways as `0`.
* Otherwise, if `obstacleGrid[0,0] = 0`, we set it to 1 and move ahead.
* Iterate the first row. If a cell originally contains a 1, this means the current cell has an obstacle and shouldn't contribute to any path. Hence, set the value of that cell to 0. Otherwise, set it to the value of previous cell i.e. `obstacleGrid[i,j] = obstacleGrid[i,j-1]`
* Iterate the first column. If a cell originally contains a 1, this means the current cell has an obstacle and shouldn't contribute to any path. Hence, set the value of that cell to 0. Otherwise, set it to the value of previous cell i.e. `obstacleGrid[i,j] = obstacleGrid[i-1,j]`
* Now, iterate through the array starting from cell obstacleGrid[1,1]. If a cell originally doesn't contain any obstacle then the number of ways of reaching that cell would be the sum of number of ways of reaching the cell above it and number of ways of reaching the cell to the left of it.
    ```
    obstacleGrid[i,j] = obstacleGrid[i-1,j] + obstacleGrid[i,j-1]
    ```
* If a cell contains an obstacle set it to 0 and continue. This is done to make sure it doesn't contribute to any other path.

```cpp
class Solution {
public:
    int uniquePathsWithObstacles(vector<vector<int>>& obstacleGrid) {
        int m = obstacleGrid.size();
        int n = obstacleGrid[0].size();
        vector<vector<int>> dp(m, vector<int>(n, 1));
        if(obstacleGrid[0][0] == 1)
            return 0;
        
        dp[0][0] = 1;
        
        for(int i = 1; i < m; ++i) {
            dp[i][0] = obstacleGrid[i][0] == 1? 0: dp[i-1][0];
        }
        for(int j = 1; j < n; ++j) {
            dp[0][j] = obstacleGrid[0][j] == 1? 0: dp[0][j-1];
        }
        
        for(int i = 1; i < m; ++i){
            for(int j = 1; j < n; ++j){
                dp[i][j] = obstacleGrid[i][j] == 1? 0: dp[i-1][j] + dp[i][j-1];
            }
        }
        return dp[m-1][n-1];
    }
};
```