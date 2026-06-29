# [Problem Link](https://www.geeksforgeeks.org/problems/matrix-chain-multiplication0303/1)

# Code❤️
# Recursion + memo 
```c++
//tc: O(n^3)
//sc O(n^2) + O(n)
class Solution {
  public:
    int f(int i,int j,vector<int>& arr,vector<vector<int>>& dp){
        if(i == j)return 0;
        if(dp[i][j] != -1)return dp[i][j];
        int operations = 0;
        int min_op = 1e9;
        for(int k=i;k<j;k++){
            operations = arr[i-1]*arr[k]*arr[j] + f(i,k,arr,dp)+f(k+1,j,arr,dp);
            min_op = min(operations,min_op);
        }
        return dp[i][j] = min_op;
    }
    int matrixMultiplication(vector<int> &arr) {
        // code here
        int n = arr.size();
        vector<vector<int>>dp(n,vector<int>(n,-1));
        return f(1,n-1,arr,dp);
    }
};
```
# tabulation
```c++
//tc: O(n^3)
//sc O(n^2) 
class Solution {
  public:
    int matrixMultiplication(vector<int> &arr) {
        // code here
        int n = arr.size();
        vector<vector<int>>dp(n,vector<int>(n,0));
      
        for(int i=n-1;i>=1;i--){
            for(int j=i+1;j<n;j++){
                  int operations = 0;
                  int min_op = 1e9;
                for(int k=i;k<j;k++){
                operations = arr[i-1]*arr[k]*arr[j] + dp[i][k]+dp[k+1][j];
                min_op = min(operations,min_op);
                }
             dp[i][j] = min_op;
            }
        }
        return dp[1][n-1];
    }
};
```