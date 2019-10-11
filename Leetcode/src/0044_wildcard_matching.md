# 44. Wildcard Matching

## Description

Given an input string (`s`) and a pattern (`p`), implement wildcard pattern matching with support for `'?'` and `'*'`.

```
'?' Matches any single character.
'*' Matches any sequence of characters (including the empty sequence).
```

The matching should cover the entire input string (not partial).

Note:

* `s` could be empty and contains only lowercase letters `a-z`.
* `p` could be empty and contains only lowercase letters `a-z`, and characters like `?` or `*`.

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
p = "*"
Output: true
Explanation: '*' matches any sequence.
```

**Example 3:**

```
Input:
s = "cb"
p = "?a"
Output: false
Explanation: '?' matches 'c', but the second letter is 'a', which does not match 'b'.
```

**Example 4:**

```
Input:
s = "adceb"
p = "*a*b"
Output: true
Explanation: The first '*' matches the empty sequence, while the second '*' matches the substring "dce".
```

**Example 5:**

```
Input:
s = "acdcb"
p = "a*c?b"
Output: false
```

## Solution

[link](https://www.geeksforgeeks.org/wildcard-pattern-matching/)

||''|a|b|*|e|
|:----:|:----:|:----:|:----:|:----:|:----:|
|**''**|T|F|F|F|F|
|**a**|F|T|F|F|F|
|**b**|F|F|T|T|F|
|**c**|F|F|F|T|F|
|**d**|F|F|F|T|F|
|**e**|F|F|F|T|T|

We can use Dynamic Programming to solve this problem

Let dp[i][j] is true if first i characters in given string matches the first j characters of pattern.

**DP Initialization:**

```
// both text and pattern are null
dp[0][0] = true; 

// pattern is null
dp[i][0] = false; 

// text is null
dp[0][j] = dp[0][j - 1] if pattern[j – 1] is '*'  
```

**DP relation :**

```cpp
// If current characters match, result is same as 
// result for lengths minus one. Characters match
// in two cases:
// a) If pattern character is '?' then it matches  
//    with any character of text. 
// b) If current characters in both match
if ( pattern[j – 1] == ‘?’) || 
     (pattern[j – 1] == text[i - 1])
    dp[i][j] = dp[i-1][j-1]   
 
// If we encounter ‘*’, two choices are possible-
// a) We ignore ‘*’ character and move to next 
//    character in the pattern, i.e., ‘*’ 
//    indicates an empty sequence. dp[i][j-1]
// b) '*' character matches with ith character in
//     input . dp[i-1][j]
else if (pattern[j – 1] == ‘*’)
    T[i][j] = T[i][j-1] || T[i-1][j]  

else // if (pattern[j – 1] != text[i - 1])
    T[i][j]  = false 
```

```cpp
class Solution {
public:
    bool isMatch(string s, string p) {
        int m = s.length();
        int n = p.length();
        vector<vector<bool>> dp(m+1, vector<bool>(n+1, false));
        dp[0][0] = true;
        
        for(int j = 1; j <= n; ++j) {
            if(p[j-1] == '*')
                dp[0][j] = dp[0][j-1];
        }
        
        for(int i = 1; i <= m; i++) {
            for(int j = 1; j <= n; j++) {
                if(s[i-1] == p[j-1] || p[j-1] == '?') {
                    dp[i][j] = dp[i-1][j-1];
                }else if(p[j-1] == '*') {
                    dp[i][j] = dp[i][j-1] || dp[i-1][j];
                }
            }
        }
        
        return dp[m][n];
    }
};
```
 