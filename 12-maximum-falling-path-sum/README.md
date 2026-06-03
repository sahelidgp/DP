# [Problem link](https://leetcode.com/problems/minimum-falling-path-sum/description/)

# Recursion + Memo
```c++
class Solution {
public:
    int min_path_sum(int row,int col,vector<vector<int>>&matrix,vector<vector<int>>& dp){
        int n = matrix.size();
        if(col == n || col<0)return 1e9;
        if(row == n-1)return matrix[row][col];
        if(dp[row][col] != 1e9)return dp[row][col];
        int left_diag = min_path_sum(row+1,col-1,matrix,dp);
        int right_diag = min_path_sum(row+1,col+1,matrix,dp);
        int down = min_path_sum(row+1,col,matrix,dp);
        return dp[row][col] = min(min(left_diag,right_diag),down) + matrix[row][col];
    }
    int minFallingPathSum(vector<vector<int>>& matrix) {
        int n = matrix.size();
        int min_sum = 1e9;
        vector<vector<int>>dp(n,vector<int>(n,1e9));
        for(int col=0;col<n;col++){
            min_sum = min(min_sum,min_path_sum(0,col,matrix,dp));
        }
        return min_sum;
    }
};
```
# Tabulation
```c++
class Solution {
public:
    int minFallingPathSum(vector<vector<int>>& matrix) {
        int n = matrix.size();
        int min_sum = 1e9;
        vector<vector<int>>dp(n,vector<int>(n,1e9));
        for(int row = 0;row < n;row++){
            for(int col = 0;col < n;col++){
                if(row == 0)dp[row][col] = matrix[row][col];
                else if(col == 0)dp[row][col] = min(dp[row-1][col],dp[row-1][col+1]) + matrix[row][col];
                else if(col == n-1)dp[row][col] = min(dp[row-1][col],dp[row-1][col-1]) + matrix[row][col];
                else dp[row][col] = min(min(dp[row-1][col-1],dp[row-1][col]),dp[row-1][col+1]) + matrix[row][col];

                if(row == n-1)min_sum = min(min_sum,dp[row][col]);
            }
        }
        return min_sum;
    }
};
```
# Space Optimization
```c++
class Solution {
public:
    int minFallingPathSum(vector<vector<int>>& matrix) {
        int n = matrix.size();
        int min_sum = 1e9;
        vector<int>prev(n,1e9);
        vector<int>temp(n);
        for(int row = 0;row < n;row++){
            for(int col = 0;col < n;col++){
                if(row == 0)temp[col] = matrix[row][col];
                else if(col == 0)temp[col] = min(prev[col],prev[col+1]) + matrix[row][col];
                else if(col == n-1)temp[col] = min(prev[col],prev[col-1]) + matrix[row][col];
                else temp[col] = min(min(prev[col-1],prev[col]),prev[col+1]) + matrix[row][col];

                if(row == n-1)min_sum = min(min_sum,temp[col]);
            }
            prev = temp;
        }
        return min_sum;
    }
};
```