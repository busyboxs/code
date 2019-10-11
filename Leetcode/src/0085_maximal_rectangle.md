# 85. Maximal Rectangle

## Description

Given a 2D binary matrix filled with 0's and 1's, find the largest rectangle containing only 1's and return its area.

**Example:**

```
Input:
[
  ["1","0","1","0","0"],
  ["1","0","1","1","1"],
  ["1","1","1","1","1"],
  ["1","0","0","1","0"]
]
Output: 6
```

## Solution

**Reference link:**

* [https://www.geeksforgeeks.org/largest-rectangle-under-histogram/](https://www.geeksforgeeks.org/largest-rectangle-under-histogram/)
* [https://www.geeksforgeeks.org/maximum-size-rectangle-binary-sub-matrix-1s/](https://www.geeksforgeeks.org/maximum-size-rectangle-binary-sub-matrix-1s/)
* [https://www.youtube.com/watch?v=g8bSdXCG-lA](https://www.youtube.com/watch?v=g8bSdXCG-lA)
* [https://www.youtube.com/watch?v=ZmnqCZp9bBs](https://www.youtube.com/watch?v=ZmnqCZp9bBs)

```cpp
class Solution {
public:
    int maximalRectangle(vector<vector<char>>& matrix) {
        if(matrix.empty())
            return 0;
        int m = matrix.size();
        int n = matrix[0].size();
        vector<int> hist(n, 0);
        int area = 0;
        int result = 0;
        for(int i = 0; i < m; ++i) {
            for(int j = 0; j < n; ++j) {
                if(matrix[i][j] == '1')
                    hist[j] += 1;
                else
                    hist[j] = 0;
            }
            area = maximalHist(hist);
            result = max(result, area);
        }
        return result;
    }
    
private:
    int maximalHist(vector<int>& row) {
        int n = row.size();
        stack<int> s;
        int max_area = 0;
        int area = 0;
        int tp = 0;
        int i = 0;
        while(i < n) {
            if(s.empty() || row[s.top()] <= row[i]) {
                s.push(i++);
            }
            else{
                tp = s.top();
                s.pop();
                if(s.empty()) {
                    area = row[tp] * i;
                }
                else {
                    area = row[tp] * (i - s.top() - 1); 
                }
                
                if(area > max_area) {
                    max_area = area;
                }
            }
        }
        
        while(!s.empty()) {
            tp = s.top();
            s.pop();
            if(s.empty()) {
                area = row[tp] * i;
            }
            else {
                area = row[tp] * (i - s.top() - 1); 
            }

            if(area > max_area) {
                max_area = area;
            }
        }
        return max_area;
    }
};
```