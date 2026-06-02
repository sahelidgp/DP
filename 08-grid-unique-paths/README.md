#  Unique Paths
# [Probem link](https://leetcode.com/problems/unique-paths/description/)
There is a robot on an m x n grid. The robot is initially located at the top-left corner (i.e., grid[0][0]). The robot tries to move to the bottom-right corner (i.e., grid[m - 1][n - 1]). The robot can only move either down or right at any point in time.

Given the two integers m and n, return the number of possible unique paths that the robot can take to reach the bottom-right corner.

The test cases are generated so that the answer will be less than or equal to 2 * 109.

 

Example 1:


Input: m = 3, n = 7
Output: 28
Example 2:

Input: m = 3, n = 2
Output: 3
Explanation: From the top-left corner, there are a total of 3 ways to reach the bottom-right corner:
1. Right -> Down -> Down
2. Down -> Down -> Right
3. Down -> Right -> Down
 

Constraints:

1 <= m, n <= 100

# Memoization + recursion

```c++
class Solution {
public:
    int count_path(int row,int col,vector<vector<int>>& dp){
        if(row == 0 && col == 0)return 1;
        if(row<0 || col<0)return 0;
        if(dp[row][col] != -1)return dp[row][col];
        int left_path = count_path(row-1,col,dp);
        int right_path = count_path(row,col-1,dp);
        return dp[row][col] = left_path + right_path;
    }
    int uniquePaths(int m, int n) {
        vector<vector<int>>dp(m,vector<int>(n,-1));
        return count_path(m-1,n-1,dp);
    }
};
```

# tabulation

```c++
class Solution {
public:
    int uniquePaths(int m, int n) {
        vector<vector<int>>dp(m,vector<int>(n,1));
        for(int row=1;row<m;row++){
            for(int col=1;col<n;col++){
                dp[row][col] = dp[row-1][col] + dp[row][col-1];
            }
        }
        return dp[m-1][n-1];
    }
};
```
# Space Optimization

```c++
class Solution {
public:
    int uniquePaths(int m, int n) {
        vector<int>prev(n,1);
        for(int row=1;row<m;row++){
            vector<int>temp(n);
            temp[0] = 1;
           for(int col=1;col<n;col++){
            temp[col] = temp[col-1] + prev[col];
           }
           prev = temp;
        }
        return prev[n-1];
    }
};
```