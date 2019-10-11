# 5. Longest Palindromic Substring

## Description

Given a string **s**, find the longest palindromic substring in **s**. You may assume that the maximum length of **s** is 1000.

Example 1:

```
Input: "babad"
Output: "bab"
Note: "aba" is also a valid answer.
```

Example 2:

```
Input: "cbbd"
Output: "bb"
```

## Solution

```cpp
class Solution {
public:
    string longestPalindrome(string s) {
        int n = s.length();
        if(n < 2)
            return s;
        for(int i = 0; i < n - 1; ++i){
            checkP(s, i, i);
            checkP(s, i, i+1);
        }
        return s.substr(start, maxLen);
    }
    
private:
    int start, maxLen;
    
    void checkP(string s, int i, int j){
        while(i >= 0 && j < s.length() && s[i] == s[j]){
            i--;
            j++;
        }
        if(maxLen < j - i - 1){
            maxLen = j - i - 1;
            start = i + 1;
        }
    }
};
```