# 557. Reverse Words in a String III

## Description

Given a string, you need to reverse the order of characters in each word within a sentence while still preserving whitespace and initial word order.

**Example 1:**

```
Input: "Let's take LeetCode contest"
Output: "s'teL ekat edoCteeL tsetnoc"
```

**Note**: In the string, each word is separated by single space and there will not be any extra space in the string.

## Solution

```cpp
class Solution {
public:
    string reverseWords(string s) {
        for(int i = 0, j = 0; i <= s.size(); ++i) {
           if(s[i] == ' ' || i == s.size()) {  // i == s.size() just for last word
               reverse(s.begin() + j, s.begin() + i);
               j = i + 1;
           }
        }
        
        return s;
    }
};
```