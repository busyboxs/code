# 412. Fizz Buzz

## Description

Write a program that outputs the string representation of numbers from 1 to n.

But for multiples of three it should output “Fizz” instead of the number and for the multiples of five output “Buzz”. For numbers which are multiples of both three and five output “FizzBuzz”.

**Example:**

```
n = 15,

Return:
[
    "1",
    "2",
    "Fizz",
    "4",
    "Buzz",
    "Fizz",
    "7",
    "8",
    "Fizz",
    "Buzz",
    "11",
    "Fizz",
    "13",
    "14",
    "FizzBuzz"
]
```

## Solution

```cpp
class Solution {
public:
    vector<string> fizzBuzz(int n) {
        vector<string> res(n);
        for(int i = 1; i <= n; ++i) {
            if(0 == i%3) {
                res[i-1] += "Fizz";
            }
            
            if(0 == i%5) {
                res[i-1] += "Buzz";
            }
            
            if(res[i-1].empty()) {
                res[i-1] = to_string(i);
            }
        }
        
        return res;
    }
};
```

```cpp
class Solution {
public:
    vector<string> fizzBuzz(int n) {
        vector<string> res(n);
        for(int i = 1;i <= n; i++) {
            res[i - 1] = to_string(i);
        }
        for(int i = 2;i < n; i += 3) {
            res[i] = "Fizz";
        }
        for(int i = 4;i < n; i += 5) {
            res[i] = "Buzz";
        }
        for(int i = 14;i < n; i += 15) {
            res[i] = "FizzBuzz";
        }
        return res;
    }
};
```