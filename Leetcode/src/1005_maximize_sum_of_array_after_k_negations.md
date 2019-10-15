# 1005. Maximize Sum Of Array After K Negations

## Description

Given an array A of integers, we **must** modify the array in the following way: we choose an `i` and replace `A[i]` with `-A[i]`, and we repeat this process `K` times in total.  (We may choose the same index `i` multiple times.)

Return the largest possible sum of the array after modifying it in this way.

**Example 1:**

```
Input: A = [4,2,3], K = 1
Output: 5
Explanation: Choose indices (1,) and A becomes [4,-2,3].
```

**Example 2:**

```
Input: A = [3,-1,0,2], K = 3
Output: 6
Explanation: Choose indices (1, 2, 2) and A becomes [3,1,0,2].
```

**Example 3:**

```
Input: A = [2,-3,-1,5,-4], K = 2
Output: 13
Explanation: Choose indices (1, 4) and A becomes [2,3,-1,5,4].
```

**Note:**

- `1 <= A.length <= 10000`
- `1 <= K <= 10000`
- `-100 <= A[i] <= 100`

## Solution

```cpp
class Solution {
public:
    int largestSumAfterKNegations(vector<int>& A, int K) {
        sort(A.begin(), A.end());
        for(int i = 0; i < A.size(); ++i) {
            if(K == 0 || A[i] >= 0)
                break;
            A[i] = -A[i];
            K--;
        }
        
        return accumulate(A.begin(), A.end(), 0) - 2 * (K%2) * *min_element(A.begin(), A.end());
    }
};
```

```cpp
class Solution {
public:
    int largestSumAfterKNegations(vector<int>& A, int K) {
        int cnt[201] = {}, num = -100;
        for (auto i : A) 
            ++cnt[i + 100];
        for (auto i = -100; i <= 100 && K; ++i) {
            if (cnt[i + 100]) {
                auto k = i < 0 ? min(K, cnt[i + 100]) : K % 2;
            cnt[-i + 100] += k;
            cnt[i + 100] -= k;
            K = i < 0 ? K - k : 0;
            }
        }
        return accumulate(begin(cnt), end(cnt), 0, [&](int s, int cnt) { return s + cnt * num++; });
    }
};
```