# 788. Rotated Digits

## Description

X is a good number if after rotating each digit individually by 180 degrees, we get a valid number that is different from X.  Each digit must be rotated - we cannot choose to leave it alone.

A number is valid if each digit remains a digit after rotation. 0, 1, and 8 rotate to themselves; 2 and 5 rotate to each other; 6 and 9 rotate to each other, and the rest of the numbers do not rotate to any other number and become invalid.

Now given a positive number N, how many numbers X from 1 to N are good?

**Example:**

```
Input: 10
Output: 4
Explanation: 
There are four good numbers in the range [1, 10] : 2, 5, 6, 9.
Note that 1 and 10 are not good numbers, since they remain unchanged after rotating.
```

**Note:**

- N  will be in range [1, 10000].

## Solution

```cpp
class Solution {
public:
    int rotatedDigits(int N) {
        int res = 0;
        vector<int> must_have  = {0, 0, 1, 0,  0, 1, 1, 0, 0, 1}; // 2, 5, 6, 9
        vector<int> cant_have = {0, 0, 0 ,1, 1, 0, 0, 1, 0, 0};  // 3, 4, 7
        
        for(int i = 1; i <= N; ++i) {
            bool cnt_m = false;  // flag of digital in must have, we should have at least one.
            bool cnt_c = false;  // flag of digital in cant have, we should have none of them.
            int num = i;
            bool flag = false;
            while(num) {
                int digit = num%10;
                if(cant_have[digit]) {
                    cnt_c = true;
                    break;
                }
                
                if(!flag && must_have[digit]) {
                    cnt_m = true;
                    flag = true;
                }
                num /= 10;
            }
            
            if(!cnt_c && cnt_m)
                res++;
        }
        
        return res;
    }
};
```