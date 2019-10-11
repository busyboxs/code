# 500. Keyboard Row

## Description

Given a List of words, return the words that can be typed using letters of alphabet on only one row's of American keyboard like the image below.

![](../images/500.png)
 
**Example:**

```
Input: ["Hello", "Alaska", "Dad", "Peace"]
Output: ["Alaska", "Dad"]
```

**Note:**

- You may use one character in the keyboard more than once.
- You may assume the input string will only contain letters of alphabet.

## Solution

```cpp
class Solution {
public:
    vector<string> findWords(vector<string>& words) {
        vector<char> str1 = {'q', 'w', 'e', 'r', 't', 'y', 'u', 'i', 'o', 'p'};
        vector<char> str2 = {'a', 's', 'd', 'f', 'g', 'h', 'j', 'k', 'l'};
        vector<char> str3 = {'z', 'x', 'c', 'v', 'b', 'n', 'm'};
        
        vector<string> res;
        
        unordered_map<char, int> hash;
        
        for(auto s: str1) {
            hash[s] = 0;
            hash[s - 'a' + 'A'] = 0;
        }
        
        for(auto s: str2) {
            hash[s] = 1;
            hash[s - 'a' + 'A'] = 1;
        }
        
        for(auto s: str3) {
            hash[s] = 2;
            hash[s - 'a' + 'A'] = 2;
        }
        
        for(auto word: words) {
            bool flag = true;
            int k = hash[word[0]];
            for(auto w: word) {
                if(k != hash[w]){
                    flag = false;
                }
            }
            if(flag)
                res.push_back(word);
            
        }
        
        return res;
    }
};
```

```cpp
class Solution {
public:
    vector<string> findWords(vector<string>& words) {
        vector<char> str1 = {'q', 'w', 'e', 'r', 't', 'y', 'u', 'i', 'o', 'p', 
                             'a', 's', 'd', 'f', 'g', 'h', 'j', 'k', 'l',
                             'z', 'x', 'c', 'v', 'b', 'n', 'm'};      
        vector<string> res;
        
        unordered_map<char, int> hash;
        
        for(int i = 0; i < str1.size(); ++i) {
            hash[str1[i] - 'a' + 'A'] = hash[str1[i]] = i <= 9 ? 0 : (i <= 18? 1 : 2);
        }
        
        for(auto word: words) {
            bool flag = true;
            int k = hash[word[0]];
            for(auto w: word) {
                if(k != hash[w]){
                    flag = false;
                }
            }
            if(flag)
                res.push_back(word);
            
        }
        
        return res;
    }
};
```