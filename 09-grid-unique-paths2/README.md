#  Unique Paths II
# [Probelem link](https://leetcode.com/problems/unique-paths-ii/description/)
You are given an m x n integer array grid. There is a robot initially located at the top-left corner (i.e., grid[0][0]). The robot tries to move to the bottom-right corner (i.e., grid[m - 1][n - 1]). The robot can only move either down or right at any point in time.

An obstacle and space are marked as 1 or 0 respectively in grid. A path that the robot takes cannot include any square that is an obstacle.

Return the number of possible unique paths that the robot can take to reach the bottom-right corner.

The testcases are generated so that the answer will be less than or equal to 2 * 109.

 

Example 1:


Input: obstacleGrid = [[0,0,0],[0,1,0],[0,0,0]]
Output: 2
Explanation: There is one obstacle in the middle of the 3x3 grid above.
There are two ways to reach the bottom-right corner:
1. Right -> Right -> Down -> Down
2. Down -> Down -> Right -> Right
Example 2:


Input: obstacleGrid = [[0,1],[0,0]]
Output: 1
 

Constraints:

m == obstacleGrid.length
n == obstacleGrid[i].length
1 <= m, n <= 100
obstacleGrid[i][j] is 0 or 1.

# Recursion+Memoization

```c++
class Solution {
public:
    int count_valid_paths(int row,int col,vector<vector<int>>& obstacleGrid,vector<vector<int>>&dp){
        if(row>=0 && col >= 0 && obstacleGrid[row][col] == 1)return 0;
        if(row == 0 && col == 0)return 1;
        if(row <0 || col <0)return 0;
        if(dp[row][col] != -1)return dp[row][col];
        int left_paths = count_valid_paths(row,col-1,obstacleGrid,dp);
        int up_paths = count_valid_paths(row-1,col,obstacleGrid,dp);

        return dp[row][col] = left_paths + up_paths;
    } 
    int uniquePathsWithObstacles(vector<vector<int>>& obstacleGrid) {
        int m = obstacleGrid.size();
        int n = obstacleGrid[0].size();
        vector<vector<int>>dp(m,vector<int>(n,-1));
        return count_valid_paths(m-1,n-1,obstacleGrid,dp);
    }
};
```
# Tabulation
```c++
class Solution {
public:

    int uniquePathsWithObstacles(vector<vector<int>>& obstacleGrid) {
        int m = obstacleGrid.size();
        int n = obstacleGrid[0].size();
        vector<vector<int>>dp(m,vector<int>(n,0));

        for(int col=0;col<n;col++){
            if(obstacleGrid[0][col]==0)
                dp[0][col] = 1;
            else break;
        }

        for(int row = 1;row<m;row++){
            for(int col = 0;col<n;col++){
                if(obstacleGrid[row][col] == 0 && col>0)dp[row][col] = dp[row-1][col]+dp[row][col-1];
                else if(obstacleGrid[row][col] == 0 && col==0)dp[row][col] = dp[row-1][col];
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

    int uniquePathsWithObstacles(vector<vector<int>>& obstacleGrid) {
        int m = obstacleGrid.size();
        int n = obstacleGrid[0].size();
        vector<int>prev(n,0);

        for(int col=0;col<n;col++){
            if(obstacleGrid[0][col]==0)
                prev[col] = 1;
            else break;
        }

        for(int row = 1;row<m;row++){
            vector<int>temp(n,0);
            for(int col = 0;col<n;col++){
                if(obstacleGrid[row][col] == 0 && col>0)temp[col] = prev[col]+temp[col-1];
                else if(obstacleGrid[row][col] == 0 && col==0)temp[col] = prev[col];
            }
            prev = temp;
        }
        return prev[n-1];
    }
};
```
