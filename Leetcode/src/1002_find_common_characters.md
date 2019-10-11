# 1002. Find Common Characters

## Description

Given an array A of strings made only from lowercase letters, return a list of all characters that show up in all strings within the list (including duplicates).  For example, if a character occurs 3 times in all strings but not 4 times, you need to include that character three times in the final answer.

You may return the answer in any order.

**Example 1:**

```
Input: ["bella","label","roller"]
Output: ["e","l","l"]
```

**Example 2:**

```
Input: ["cool","lock","cook"]
Output: ["c","o"]
``` 

**Note:**

- 1 <= A.length <= 100
- 1 <= A[i].length <= 100
- A[i][j] is a lowercase letter

## Solution

```cpp
class Solution {
public:
    vector<string> commonChars(vector<string>& A) {
        vector<int> cnt(26, INT_MAX);  // 保存共有字符的计数 vector
        vector<string> res;
        
        for(auto s: A) {
            vector<int> cnt1(26, 0);  // 其中一个字符串中字符计数
            for(auto c : s) {
                ++cnt1[c - 'a'];
            }
            for(int i = 0; i < 26; ++i)
                cnt[i] = min(cnt[i], cnt1[i]);
        }
        
        for(int i = 0; i < 26; ++i)
            res.insert(res.end(), cnt[i], string(1, i+'a'));
        
        return res;
    }
};
```