# 1189. Maximum Number of Balloons

## Description

Given a string text, you want to use the characters of text to form as many instances of the word **"balloon"** as possible.

You can use each character in text **at most once**. Return the maximum number of instances that can be formed.

**Example 1:**

![](../images/1189_1.jpg)

```
Input: text = "nlaebolko"
Output: 1
```

**Example 2:**

![](../images/1189_2.jpg)

```
Input: text = "loonbalxballpoon"
Output: 2
```

**Example 3:**

```
Input: text = "leetcode"
Output: 0
```

**Constraints:**

- `1 <= text.length <= 10^4`
- text consists of lower case English letters only.

## Solution

```cpp
class Solution {
public:
    int maxNumberOfBalloons(string text) {
        unordered_map<char, int> hash;
        for(auto ch: text) {
            ++hash[ch];
        }
        
        return min({hash['b'], hash['a'], hash['l']/2, hash['o']/2, hash['n']});
    }
};
```