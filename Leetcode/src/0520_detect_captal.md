# 520. Detect Capital

## Description

Given a word, you need to judge whether the usage of capitals in it is right or not.

We define the usage of capitals in a word to be right when one of the following cases holds:

- All letters in this word are capitals, like `"USA"`.
- All letters in this word are not capitals, like `"leetcode"`.
- Only the first letter in this word is capital, like `"Google"`.

Otherwise, we define that this word doesn't use capitals in a right way.

**Example 1:**

```
Input: "USA"
Output: True
```

**Example 2:**

```
Input: "FlaG"
Output: False
```

**Note**: The input will be a non-empty word consisting of uppercase and lowercase latin letters.

## Solution

```cpp
class Solution {
public:
    bool detectCapitalUse(string word) {
        // count upper charactars 
        int cnt = count_if(word.begin(), word.end(), [](char c){return isupper(c);});
        // for case 2, case 3 and case 1
        return (cnt == 0)|| (cnt == word.length()) || (cnt == 1 && isupper(word[0])) ;
    }
};
```