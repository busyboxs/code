# 852. Peak Index in a Mountain Array

## Description

Let's call an array `A` a mountain if the following properties hold:

* A.length >= 3
* There exists some 0 < i < A.length - 1 such that `A[0] < A[1] < ... A[i-1] < A[i] > A[i+1] > ... > A[A.length - 1]`
* Given an array that is definitely a mountain, return any i such that `A[0] < A[1] < ... A[i-1] < A[i] > A[i+1] > ... > A[A.length - 1]`.

**Example 1:**

```
Input: [0,1,0]
Output: 1
```

**Example 2:**

```
Input: [0,2,1,0]
Output: 1
```

**Note:**

- `3 <= A.length <= 10000`
- `0 <= A[i] <= 10^6`
- A is a mountain, as defined above.

## Solution

```cpp
class Solution {
public:
    int peakIndexInMountainArray(vector<int>& A) {
        int l = 0, r = A.size() - 1, mid;
        while(l < r) {
            mid = l + (r - l)/2;
            if(A[mid-1] < A[mid] && A[mid] < A[mid+1])
                l = mid + 1;
            else if(A[mid-1] > A[mid] && A[mid] > A[mid+1])
                r = mid - 1;
            else
                l = r = mid;
        }
        
        return l;
    }
};
```