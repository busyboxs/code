# 961. N-Repeated Element in Size 2N Array

## Description

In a array A of size 2N, there are N+1 unique elements, and exactly one of these elements is repeated N times.

Return the element repeated N times.

**Example 1:**

```
Input: [1,2,3,3]
Output: 3
```

**Example 2:**

```
Input: [2,1,2,5,3,2]
Output: 2
```

**Example 3:**

```
Input: [5,1,5,2,5,3,5,4]
Output: 5
```

**Note:**

- 4 <= A.length <= 10000
- 0 <= A[i] < 10000
- A.length is even

## Solution

```cpp
class Solution {
public:
    int repeatedNTimes(vector<int>& A) {
        unordered_map<int, int> map;
        for(int& a: A) {
            map[a]++;
            if(map[a] >= 2)
                return a;
        }
        
        return 0;
    }
};
```

```cpp
class Solution {
public:
    int repeatedNTimes(vector<int>& A) {
        unordered_set<int> temp;
        for(int& a: A) {
            if(temp.find(a) != temp.end())
                return a;
            temp.insert(a);
        }
        
        return 0;
    }
};
```