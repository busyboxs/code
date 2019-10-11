# 1030. Matrix Cells in Distance Order

## Description

We are given a matrix with `R` rows and `C` columns has cells with integer coordinates `(r, c)`, where `0 <= r < R` and `0 <= c < C`.

Additionally, we are given a cell in that matrix with coordinates `(r0, c0)`.

Return the coordinates of all cells in the matrix, sorted by their distance from `(r0, c0)` from smallest distance to largest distance.  Here, the distance between two cells `(r1, c1)` and `(r2, c2)` is the Manhattan distance, `|r1 - r2| + |c1 - c2|`.  (You may return the answer in any order that satisfies this condition.)

**Example 1:**

```
Input: R = 1, C = 2, r0 = 0, c0 = 0
Output: [[0,0],[0,1]]
Explanation: The distances from (r0, c0) to other cells are: [0,1]
```

**Example 2:**

```
Input: R = 2, C = 2, r0 = 0, c0 = 1
Output: [[0,1],[0,0],[1,1],[1,0]]
Explanation: The distances from (r0, c0) to other cells are: [0,1,1,2]
The answer [[0,1],[1,1],[0,0],[1,0]] would also be accepted as correct.
```

**Example 3:**

```
Input: R = 2, C = 3, r0 = 1, c0 = 2
Output: [[1,2],[0,2],[1,1],[0,1],[1,0],[0,0]]
Explanation: The distances from (r0, c0) to other cells are: [0,1,1,2,2,3]
There are other answers that would also be accepted as correct, such as [[1,2],[1,1],[0,2],[1,0],[0,1],[0,0]].
```

**Note:**

- `1 <= R <= 100`
- `1 <= C <= 100`
- `0 <= r0 < R`
- `0 <= c0 < C`

## Solution

```cpp
class Solution {
public:
    vector<vector<int>> allCellsDistOrder(int R, int C, int r0, int c0) {
        /*
        1. Increment the distance from 0 till R + C.
        2. From our point, generate all points with the distance.
        3. Add valid poits (within our grid) to the result.
        */
        vector<vector<int>> res = { {r0, c0} }; // init with given point
        
        // find max distance
        // r0 + c0 means distance between point(0, 0) and point(r0, c0), i.e. left top point
        // c0 + R - r0 means distance between point(R, 0) and point(r0, c0), i.e. left bottom point
        // r0 + C - c0 means distance between point(0, C) and point(r0, c0), i.e. right top point
        // R - r0 + C - c0 means distance between point(R, C) and point(r0, c0), i.e. right bottom point
        int max_d = max({r0 + c0, c0 + R - r0, r0 + C - c0, R - r0 + C - c0});
        
        for(int d = 1; d <= max_d; ++d) {
            for(int x = d; x >= -d; --x) { // form up rows to bottom rows
                auto r1 = r0 + x; 
                auto c1_a = c0 + d - abs(x); // right columns
                auto c1_b = c0 + abs(x) - d; // left columns
                
                if( r1 >= 0 && r1 < R) {
                    if(c1_a >= 0 && c1_a < C) // need c1_a >= 0? I think c1_a is always > c0.
                        res.push_back({r1, c1_a});
                    if(c1_a != c1_b && c1_b >= 0 && c1_b < C) // need c1_b < C? I think c1_b always < c0.
                        res.push_back({r1, c1_b});
                }
            }
        }
        
        return res;
    }
};
```

We can also use BFS.