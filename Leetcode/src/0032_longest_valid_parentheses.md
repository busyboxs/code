# 32. Longest Valid Parentheses

## 题目描述

Given a string containing just the characters '(' and ')', find the length of the longest valid (well-formed) parentheses substring.

**Example 1**:

```
Input: "(()"
Output: 2
Explanation: The longest valid parentheses substring is "()"
```

**Example 2:**

```
Input: ")()())"
Output: 4
Explanation: The longest valid parentheses substring is "()()"
```

## 解题思路

参考链接： [https://leetcode.com/problems/longest-valid-parentheses/solution/](https://leetcode.com/problems/longest-valid-parentheses/solution/)

### Approach 1: Using Dynamic Programming

```cpp
class Solution {
public:
    int longestValidParentheses(string s) {
        int res = 0;
        int n = s.size();
        vector<int> dp(n, 0);
        
        for(int i = 1; i < n; ++i) {
            if(s[i] == ')') {
                if(s[i-1] == '(') {
                    dp[i] = (i>=2?dp[i-2]:0) + 2;
                }else if( i-dp[i-1] > 0 && s[i-dp[i-1]-1] == '('){
                    dp[i] = dp[i-1] + 2 + ((i-dp[i-1])>=2?dp[i-dp[i-1]-2]:0);
                }
                res = max(dp[i], res);
            }
        }
        return res;
    }
};
```


### Approach 2: Using Stack

```cpp
class Solution {
public:
    int longestValidParentheses(string s) {
        stack<int> st;
        st.push(-1);
        int res = 0;
        for(int i = 0; i < s.length(); ++i) {
            if(st.size() > 1 && s[i] == ')' && s[st.top()] == '(') {
                st.pop();
                res = max(res, i - st.top());
            }else {
                st.push(i);
            }
        } 
        return res;
    }
};
```