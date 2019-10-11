# 977. Squares of a Sorted Array

## Description

Given an array of integers A sorted in non-decreasing order, return an array of the squares of each number, also in sorted non-decreasing order.

**Example 1:**

```
Input: [-4,-1,0,3,10]
Output: [0,1,9,16,100]
```

**Example 2:**

```
Input: [-7,-3,2,3,11]
Output: [4,9,9,49,121]
```

**Note:**

* 1 <= A.length <= 10000
* -10000 <= A[i] <= 10000
* A is sorted in non-decreasing order.

## Solution

```cpp
class Solution {
public:
    vector<int> sortedSquares(vector<int>& A) {
        int n = A.size();
        vector<int> result;
        if(n == 1){
            return {A[0]*A[0]};
        }
        if(A[0] >= 0) {
            for(auto a: A) {
                result.push_back(a*a);
            }
            return result;
        }else {
            int e = 0;
            int s = 0;
            for(int i = 0; i < n; ++i) {
                if (A[i] >= 0) {
                    e = i;
                    s = e - 1;
                    break;
                }
            }
            while(s >= 0 && e < n) {
                if (A[s]*A[s] > A[e]*A[e]) {
                    result.push_back(A[e]*A[e]);
                    e++;
                }else{
                    result.push_back(A[s]*A[s]);
                    s--;
                }
            }
            while(s >= 0){
                result.push_back(A[s]*A[s]);
                s--;
            }
            while(e < n) {
                result.push_back(A[e]*A[e]);
                e++;
            }
            return result;
        }
    }
};
```