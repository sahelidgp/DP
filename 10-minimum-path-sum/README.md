#  Minimum Path Sum
# [problem link](https://leetcode.com/problems/minimum-path-sum/description/)
Given a m x n grid filled with non-negative numbers, find a path from top left to bottom right, which minimizes the sum of all numbers along its path.

Note: You can only move either down or right at any point in time.

 

Example 1:


Input: grid = [[1,3,1],[1,5,1],[4,2,1]]
Output: 7
Explanation: Because the path 1 → 3 → 1 → 1 → 1 minimizes the sum.
Example 2:

Input: grid = [[1,2,3],[4,5,6]]
Output: 12
 

Constraints:

m == grid.length
n == grid[i].length
1 <= m, n <= 200
0 <= grid[i][j] <= 200

# Recursion+ Memoization

```c++
class Solution {
public:
    int path_sum(int row,int col,vector<vector<int>>& grid,vector<vector<int>>& dp){
        if(row == 0 && col == 0)return grid[row][col];
        if(row<0 || col <0)return 1e9;

        if(dp[row][col] != -1)return dp[row][col];

        int left_sum = path_sum(row-1,col,grid,dp);
        int right_sum = path_sum(row,col-1,grid,dp);

        return dp[row][col] = min(left_sum,right_sum) + grid[row][col];
    }
    int minPathSum(vector<vector<int>>& grid) {
        int n = grid.size();
        int m = grid[0].size();
        vector<vector<int>>dp(n,vector<int>(m,-1));
        return path_sum(n-1,m-1,grid,dp);
    }
};
```

# Tabulation

```c++
class Solution {
public:
    int minPathSum(vector<vector<int>>& grid) {
        int n = grid.size();
        int m = grid[0].size();
        vector<vector<int>>dp(n,vector<int>(m,0));
        for(int row = 0;row < n;row++){
            for(int col = 0;col < m;col++){
                if(row == 0 && col == 0)dp[row][col] = grid[row][col];
                else if(row ==  0)dp[row][col] = dp[row][col-1] + grid[row][col];
                else if(col == 0)dp[row][col] = dp[row-1][col] + grid[row][col];
                else dp[row][col] = min(dp[row-1][col],dp[row][col-1]) + grid[row][col];
            }
        }
        return dp[n-1][m-1];
    }
};
```
# Space Optimization
```c++
class Solution {
public:
    int minPathSum(vector<vector<int>>& grid) {
        int n = grid.size();
        int m = grid[0].size();
        vector<int>prev(m,0);
         vector<int>temp(m,0);
        for(int row = 0;row < n;row++){
           
            for(int col = 0;col < m;col++){
                if(row == 0 && col == 0)temp[col] = grid[row][col];
                else if(row ==  0)temp[col] = temp[col-1] + grid[row][col];
                else if(col == 0)temp[col] = prev[col] + grid[row][col];
                else temp[col] = min(prev[col],temp[col-1]) + grid[row][col];
            }
            prev = temp;
        }
        return prev[m-1];
    }
};
```