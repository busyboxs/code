# 1185. Day of the Week

## Description

Given a date, return the corresponding day of the week for that date.

The input is given as three integers representing the `day`, `month` and `year` respectively.

Return the answer as one of the following values `{"Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"}`.

**Example 1:**

```
Input: day = 31, month = 8, year = 2019
Output: "Saturday"
```

**Example 2:**

```
Input: day = 18, month = 7, year = 1999
Output: "Sunday"
```

**Example 3:**

```
Input: day = 15, month = 8, year = 1993
Output: "Sunday"
```

**Constraints:**

- The given dates are valid dates between the years 1971 and 2100.

## Solution

```cpp
class Solution {
public:
    string dayOfTheWeek(int day, int month, int year) {
        vector<string> week = {"Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"};
        if(month < 3) {
            month += 12;
            year--;
        }
        int w = (day + 2*month + 3*(month+1)/5 + year + year/4 - year/100 + year/400 + 1)%7;
        return week[w];
    }
};
```