# 447. Number of Boomerangs

## Description

Given n points in the plane that are all pairwise distinct, a "boomerang" is a tuple of points `(i, j, k)` such that the distance between `i` and `j` equals the distance between i and k (**the order of the tuple matters**).

Find the number of boomerangs. You may assume that n will be at most **500** and coordinates of points are all in the range **[-10000, 10000]** (inclusive).

**Example:**

```
Input:
[[0,0],[1,0],[2,0]]

Output:
2

Explanation:
The two boomerangs are [[1,0],[0,0],[2,0]] and [[1,0],[2,0],[0,0]]
```

## Solution

```cpp
class Solution {
public:
    int numberOfBoomerangs(vector<vector< int>>& points) {
        int booms = 0;
        for (auto &p : points) {
            unordered_map<int, int> distance(points.size()); // sa for one point, there only has at most points.size() distance
            for (auto &q : points){
                // 为什么这里是乘以 2 呢？
                // 假设第一个 for 中的 q 为中心点，则需要找到左边和右边的点，使得到中心点距离相等
                // 首先初始化 map 为 0， size 为 points 中点的数量（最多只会得到这么多个距离）
                // 然后开始求解， 以距离为 4 来说明。 首先 distance[4] = 0;
                // 然后有点与 p 距离为4，由于原来 distance[4] = 0，即没有与 p 距离为 4，则结果 res += 0 (booms += 2 * distance[4] )，然后 distance[4] 加 1， distance[4] = 1;
                // 然后再有一个点与 p 距离为 4 时，可以将该点放在左边或者右边（因此*2），而剩下的一个点从 distance 为 4 的点中取，总共有 distance[4] 种；因此 总的结果为 2 * distance[4]，然后 distance[4] 再加 1.
                booms += 2 * distance[pow((p[0] - q[0]), 2) + pow((p[1] - q[1]), 2)]++;
            }
        }
        return booms;
    }
};
```