# 1021. Remove Outermost Parentheses

A valid parentheses string is either empty `("")`, `"(" + A + ")"`, or `A + B`, where `A` and `B` are valid parentheses strings, and + represents string concatenation.  For example, `""`, `"()"`, `"(())()"`, and `"(()(()))"` are all valid parentheses strings.

A valid parentheses string `S` is **primitive** if it is nonempty, and there does not exist a way to split it into `S = A+B`, with `A` and `B` nonempty valid parentheses strings.

Given a valid parentheses string S, consider its primitive decomposition: `S = P_1 + P_2 + ... + P_k`, where `P_i` are primitive valid parentheses strings.

Return `S` after removing the outermost parentheses of every primitive string in the primitive decomposition of `S`.

**Example 1:**

```
Input: "(()())(())"
Output: "()()()"
Explanation: 
The input string is "(()())(())", with primitive decomposition "(()())" + "(())".
After removing outer parentheses of each part, this is "()()" + "()" = "()()()".
```

**Example 2:**

```
Input: "(()())(())(()(()))"
Output: "()()()()(())"
Explanation: 
The input string is "(()())(())(()(()))", with primitive decomposition "(()())" + "(())" + "(()(()))".
After removing outer parentheses of each part, this is "()()" + "()" + "()(())" = "()()()()(())".
```

**Example 3:**

```
Input: "()()"
Output: ""
Explanation: 
The input string is "()()", with primitive decomposition "()" + "()".
After removing outer parentheses of each part, this is "" + "" = "".
```

**Note:**

- `S.length <= 10000`
- `S[i]` is `"("` or `")"`
- S is a valid parentheses string

## Solution

```cpp
class Solution {
public:
    string removeOuterParentheses(string S) {
        int cnt_l = 0, cnt_r = 0, start = 0;
        const int len = S.length();
        string res;
        
        for(int i = 0; i < len; ++i) {
            if(S[i] == '(')
                cnt_l++;
            else
                cnt_r++;
            
            if(cnt_l == cnt_r) {
                res.append(S.substr(start+1, i-start-1));
                start = i + 1;
            }
        }
        
        return res;
    }
};
```