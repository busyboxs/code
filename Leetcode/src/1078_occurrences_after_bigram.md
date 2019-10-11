# 1078. Occurrences After Bigram

## Description

Given words `first` and `second`, consider occurrences in some `text` of the form `"first second third"`, where `second` comes immediately after `first`, and `third` comes immediately after `second`.

For each such occurrence, add `"third"` to the answer, and return the `answer`.

**Example 1:**

```
Input: text = "alice is a good girl she is a good student", first = "a", second = "good"
Output: ["girl","student"]
```

**Example 2:**

```
Input: text = "we will we will rock you", first = "we", second = "will"
Output: ["we","rock"]
```

**Note:**

- `1 <= text.length <= 1000`
- `text` consists of space separated words, where each word consists of lowercase English letters.
- `1 <= first.length, second.length <= 10`
- `first` and `second` consist of lowercase English letters.

## Solution

```cpp
class Solution {
public:
    vector<string> findOcurrences(string text, string first, string second) {
        vector<string> res;
        string bigram = " " + first + " " + second + " ";
        text = " " + text;
        auto p = text.find(bigram);
        
        while(p != string::npos) {
            auto p1 = p + bigram.length();
            auto p2 = p1;
            while(p2 < text.length() && text[p2] != ' ')
                p2++;
            res.push_back(text.substr(p1, p2 - p1));
            p = text.find(bigram, p + 1);
        }
        
        return res;
    }
};
```