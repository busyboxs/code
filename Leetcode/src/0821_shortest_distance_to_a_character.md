# 821. Shortest Distance to a Character

## Description

Given a string `S` and a character `C`, return an array of integers representing the shortest distance from the character `C` in the string.

**Example 1:**

```
Input: S = "loveleetcode", C = 'e'
Output: [3, 2, 1, 0, 1, 0, 0, 1, 2, 2, 1, 0]
```

**Note:**

- `S` string length is in `[1, 10000]`.
- `C` is a single character, and guaranteed to be in string `S`.
- All letters in `S` and `C` are lowercase.

## Solution

```cpp
class Solution {
public:
    vector<int> shortestToChar(string S, char C) {
        int n = S.length();
        vector<int> res(n, n);
        // pos = -n to make (i - pos) >= n;
        // rpos = 2*n to make (rpos - (n-1-i)) >= n;
        int pos = -n, rpos = 2*n;
        
        for(int i = 0; i < n; ++i) {
            if(S[i] == C)
                pos = i;
            // get the right value on the right of pos and pos.
            // eg. for loveleetcode" and 'e' we can get
            // right res: [n, n, n, 0, 1, 0, 0, 1, 2, 3, 4, 0]
            res[i] = min(res[i], abs(i - pos));  
            
            if(S[n-1-i] == C)
                rpos = n-1-i;
            // get the right value on the left of rpos and rpos.
            // eg. for loveleetcode" and 'e' we can get
            // right res: [n, n, n, 0, 1, 0, 0, 1, 2, 3, 4, 0]
            // left  res: [3, 2, 1, 0, 1, 0, 0, 4, 3, 2, 1, 0]
            // final res: [3, 2, 1, 0, 1, 0, 0, 1, 2, 2, 1, 0]
            res[n-1-i] = min(res[n-1-i], abs(rpos - (n - 1 -i)));  
        }
        
        return res;
        
    }
};
```