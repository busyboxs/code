# 242. Valid Anagram

## Description

Given two strings s and t , write a function to determine if t is an anagram of s.

**Example 1:**

```
Input: s = "anagram", t = "nagaram"
Output: true
```

**Example 2:**

```
Input: s = "rat", t = "car"
Output: false
```

**Note:**

- You may assume the string contains only lowercase alphabets.

**Follow up:**

- What if the inputs contain unicode characters? How would you adapt your solution to such case?

## Solution

```cpp
class Solution {
public:
    bool isAnagram(string s, string t) {
        if(s.length() != t.length())
            return false;
        vector<int> count(26, 0);
        for(int i = 0; i < s.length(); ++i) {
            count[s[i] - 'a'] ++;
            count[t[i] - 'a'] --;
        }
        for(int i = 0; i < count.size(); ++i) {
            if(count[i])
            return false;
        }
        
        return true;
    }
};
```

```cpp
class Solution {
public:
    bool isAnagram(string s, string t) {
        if(s.length() != t.length())
            return false;
        vector<int> count(26, 0);
        for(int i = 0; i < s.length(); ++i) {
            count[s[i] - 'a'] ++;
            count[t[i] - 'a'] --;
        }
        
        return all_of(count.begin(), count.end(), [](int i){return i == 0;});
    }
};
```