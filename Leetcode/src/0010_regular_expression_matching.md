# 10. Regular Expression Matching

## 题目描述

Given an input string (`s`) and a pattern (`p`), implement regular expression matching with support for `'.'` and `'*'`.

```
'.' Matches any single character.
'*' Matches zero or more of the preceding element.
```

The matching should cover the entire input string (not partial).

**Note:**

* `s` could be empty and contains only lowercase letters `a-z`.
* `p` could be empty and contains only lowercase letters `a-z`, and characters like `.` or `*`.

**Example 1:**

```
Input:
s = "aa"
p = "a"
Output: false
Explanation: "a" does not match the entire string "aa".
```

**Example 2:**

```
Input:
s = "aa"
p = "a*"
Output: true
Explanation: '*' means zero or more of the precedeng element, 'a'. Therefore, by repeating 'a' once, it becomes "aa".
```

**Example 3:**

```
Input:
s = "ab"
p = ".*"
Output: true
Explanation: ".*" means "zero or more (*) of any character (.)".
```

**Example 4:**

```
Input:
s = "aab"
p = "c*a*b"
Output: true
Explanation: c can be repeated 0 times, a can be repeated 1 time. Therefore it matches "aab".
```

**Example 5:**

```
Input:
s = "mississippi"
p = "mis*is*p*."
Output: false
```

## 解题思路

参考链接： [https://youtu.be/l3hda49XcDE](https://youtu.be/l3hda49XcDE)

动态规划

```cpp
class Solution {
public:
    bool isMatch(string s, string p) {
        int m = s.length();
        int n = p.length();
        vector<vector<bool>> dp(m+1, vector<bool>(n+1, false));
        dp[0][0] = true; // both string are empty
        
        //deal with pattern like a* or a*b* or a*b*c*
        for(int i = 1; i <= n; ++i) {
            if(p[i-1] == '*')
                dp[0][i] = dp[0][i-2];
        }
        for(int i = 1; i <= m; ++i) {
            for(int j = 1; j <= n; ++j) {
                if(s[i-1] == p[j-1] || p[j-1] == '.') {
                    dp[i][j] = dp[i-1][j-1];
                }else if(p[j-1] == '*') {
                    dp[i][j] = dp[i][j-2]; // match 0 times
                    if(s[i-1] == p[j-2] || p[j-2] == '.') {
                        // dp[i-1][j]表示去掉s的最后一个字符，看剩下的是否匹配，因为*匹配了至少一次（1~k），去掉之后就是匹配（0 ~ k-1)次。
                        dp[i][j] = dp[i][j] || dp[i-1][j];
                    }
                }
            }
        }
        return dp[m][n];
    }
};
```