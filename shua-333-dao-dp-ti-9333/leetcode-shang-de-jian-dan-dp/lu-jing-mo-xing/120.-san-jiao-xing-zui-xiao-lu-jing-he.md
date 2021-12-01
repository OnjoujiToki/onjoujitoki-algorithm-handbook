---
description: 数字三角形模型模板题
---

# 120. 三角形最小路径和

Given a `triangle` array, return _the minimum path sum from top to bottom_.

For each step, you may move to an adjacent number of the row below. More formally, if you are on index `i` on the current row, you may move to either index `i` or index `i + 1` on the next row.

**Example 1:**

```
Input: triangle = [[2],[3,4],[6,5,7],[4,1,8,3]]Output: 11Explanation: The triangle looks like:   2  3 4 6 5 74 1 8 3The minimum path sum from top to bottom is 2 + 3 + 5 + 1 = 11 (underlined above).
```

**Example 2:**

```
Input: triangle = [[-10]]Output: -10 
```

**Constraints:**

* `1 <= triangle.length <= 200`
* `triangle[0].length == 1`
* `triangle[i].length == triangle[i - 1].length + 1`
* `-104 <= triangle[i][j] <= 104`

**Follow up:** Could you do this using only `O(n)` extra space, where `n` is the total number of rows in the triangle?

```clike
class Solution {
public:
    int minimumTotal(vector<vector<int>>& triangle) {
        if (triangle.size() == 0) return 0;
        if (triangle.size() == 1) return triangle[0][0];
        int m = triangle.size();
        int n = triangle.back().size();
        vector<vector<int>> dp(2, vector<int> (n, 0));
        dp[0][0] = triangle[0][0];
        int curRes = INT_MAX;
        // dp[i][j] = dp[i-1][j-1] + dp[i-1][j] 
        for (int i = 1; i < m; i++) {
            for (int j = 0; j <= i; j++) {
                dp[i&1][j] = triangle[i][j];
                if (j == 0) dp[i&1][j] += dp[i-1&1][j];
                else if (j == i) dp[i&1][j] += dp[i-1&1][j-1];
                else dp[i&1][j] += min(dp[i-1&1][j], dp[i-1&1][j-1]);
                if (i == m-1) curRes = min(dp[i&1][j], curRes);
            }                         
        }       
        return curRes;
    }
};
```

坑：滚动数组的最后一行不一定是最后结论，要看行数奇偶。所以最后输出答案的时候有2个方法，一个是根据奇偶判断在第一行还是第二行，另外一个就是像这样特判i记录最小结果即可。
