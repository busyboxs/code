# 1013. Partition Array Into Three Parts With Equal Sum

## Description

Given an array A of integers, return true if and only if we can partition the array into three non-empty parts with equal sums.

Formally, we can partition the array if we can find indexes `i+1 < j` with `(A[0] + A[1] + ... + A[i] == A[i+1] + A[i+2] + ... + A[j-1] == A[j] + A[j-1] + ... + A[A.length - 1])`

**Example 1:**

```
Input: [0,2,1,-6,6,-7,9,1,2,0,1]
Output: true
Explanation: 0 + 2 + 1 = -6 + 6 - 7 + 9 + 1 = 2 + 0 + 1
```

**Example 2:**

```
Input: [0,2,1,-6,6,7,9,-1,2,0,1]
Output: false
```

**Example 3:**

```
Input: [3,3,6,5,-2,2,5,1,-9,4]
Output: true
Explanation: 3 + 3 = 6 = 5 - 2 + 2 + 5 + 1 - 9 + 4
```

**Note:**

- `3 <= A.length <= 50000`
- `-10000 <= A[i] <= 10000`

## Solution

```cpp
class Solution {
public:
    bool canThreePartsEqualSum(vector<int>& A) {
        int total = accumulate(A.begin(), A.end(), 0);
        if(total%3)
            return false;
        for(int i = 0, sum = 0; i < A.size(); ++i) {
            sum += A[i];
            if(sum == (parts+1)*total/3)
                ++parts;
        }
        
        return parts >= 3;
    }
};
```

```cpp
class Solution {
public:
    bool canThreePartsEqualSum(vector<int>& A) {
        int total = accumulate(A.begin(), A.end(), 0);
        if(total%3)
            return false;
        int each = total/3;
        int sum = each;
        int count = 0;
        // idea: we should have at least 3 parts that sum = total/3
        for(auto a: A) {
            sum -= a;
            if(sum == 0){
                sum = each;
                count++;
                if(count >= 3)
                    return true;
            }    
        }
        
        return count >= 3;
    }
};
```