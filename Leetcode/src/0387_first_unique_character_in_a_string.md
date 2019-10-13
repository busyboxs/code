# 387. First Unique Character in a String

## Description

Given a string, find the first non-repeating character in it and return it's index. If it doesn't exist, return -1.

**Examples:**

```
s = "leetcode"
return 0.

s = "loveleetcode",
return 2.
```

**Note:** You may assume the string contain only lowercase letters.

## Solution

```cpp
class Solution {
public:
    int firstUniqChar(string s) {
        unordered_map<char, int> hash;
        int res = s.size();
        for(int i = 0; i < s.size(); ++i) {
            if(hash.find(s[i]) == hash.end()) {
                hash[s[i]] = i;
            }else {
                hash[s[i]] = s.size();
            }
        }
        for(auto h : hash) {
            res = min(h.second, res);
        }
        return res == s.size()? -1: res;
    }
};
```