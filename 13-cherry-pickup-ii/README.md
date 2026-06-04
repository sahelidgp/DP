# [Problem link](https://leetcode.com/problems/cherry-pickup-ii/description/)

# Recursion+Memoization

```c++
class Solution {
public:
    int path_sum(int row,int col1,int col2,vector<vector<int>>& grid,vector<vector<vector<int>>>&dp){
        int n = grid.size();
        int m = grid[0].size();
        if(col1 < 0 || col1 == m || col2 < 0 || col2 == m)return -1e9;
        if(row == n-1){
            if(col1 == col2)
            return grid[row][col1];
            else return grid[row][col1] + grid[row][col2];
        }
        if(dp[row][col1][col2] != -1)return dp[row][col1][col2];
        int maxi = -1e9;
        for(int dcol1 = -1;dcol1 <= 1;dcol1++){
            for(int dcol2 = -1;dcol2 <= 1;dcol2++){
                int nCol1 = col1 + dcol1;
                int nCol2 = col2 + dcol2;
                int value = 0;
                if(col1 == col2)value = grid[row][col1] + path_sum(row+1,nCol1,nCol2,grid,dp);
                else value = grid[row][col1] + grid[row][col2] + path_sum(row+1,nCol1,nCol2,grid,dp);
                maxi = max(maxi,value);

            }
        }
        return dp[row][col1][col2] = maxi;
    }
    int cherryPickup(vector<vector<int>>& grid) {
        int n = grid.size();
        int m = grid[0].size();
        vector<vector<vector<int>>>dp(n,vector<vector<int>>(m,vector<int>(m,-1)));
        return path_sum(0,0,m-1,grid,dp);
    }
};
```

# Tabulation

```c++
class Solution {
public:
    int cherryPickup(vector<vector<int>>& grid) {
        int n = grid.size();
        int m = grid[0].size();
        vector<vector<vector<int>>>dp(n,vector<vector<int>>(m,vector<int>(m,0)));

        //base case

        for(int col1 = 0;col1 < m;col1++){
            for(int col2 = 0;col2 < m;col2++){
                if(col1 == col2)dp[n-1][col1][col2] = grid[n-1][col1];
                else dp[n-1][col1][col2] = grid[n-1][col1] + grid[n-1][col2];
            }
        }
        //explore
        for(int row = n-2;row >= 0;row--){
            for(int col1 = 0;col1 < m;col1++){
                for(int col2 = 0;col2 < m;col2++){
                     int maxi = -1e9;
                    for(int dcol1 = -1;dcol1 <= 1;dcol1++){
                        for(int dcol2 = -1;dcol2 <= 1;dcol2++){
                            int nCol1 = col1 + dcol1;
                            int nCol2 = col2 + dcol2;
                            int value = 0;
                            if(col1 == col2)value = grid[row][col1];
                            else value = grid[row][col1] + grid[row][col2];

                            if(nCol1 >=0 && nCol1 <m && nCol2 >=0 && nCol2 < m)value += dp[row+1][nCol1][nCol2];
                            else value += -1e9;
                            maxi = max(maxi,value);

                        }
                    }
                     dp[row][col1][col2] = maxi;
                }
               
            }
          
        }
        return dp[0][0][m-1];
    }
};
```

# Space Optimization

```c++
class Solution {
public:
    int cherryPickup(vector<vector<int>>& grid) {
        int n = grid.size();
        int m = grid[0].size();
        vector<vector<int>>next(m,vector<int>(m,0));
        vector<vector<int>>temp(m,vector<int>(m,0));

        //base case

        for(int col1 = 0;col1 < m;col1++){
            for(int col2 = 0;col2 < m;col2++){
                if(col1 == col2)next[col1][col2] = grid[n-1][col1];
                else next[col1][col2] = grid[n-1][col1] + grid[n-1][col2];
            }
        }
        //explore
        for(int row = n-2;row >= 0;row--){
            for(int col1 = 0;col1 < m;col1++){
                for(int col2 = 0;col2 < m;col2++){
                     int maxi = -1e9;
                    for(int dcol1 = -1;dcol1 <= 1;dcol1++){
                        for(int dcol2 = -1;dcol2 <= 1;dcol2++){
                            int nCol1 = col1 + dcol1;
                            int nCol2 = col2 + dcol2;
                            int value = 0;
                            if(col1 == col2)value = grid[row][col1];
                            else value = grid[row][col1] + grid[row][col2];

                            if(nCol1 >=0 && nCol1 <m && nCol2 >=0 && nCol2 < m)value += next[nCol1][nCol2];
                            else value += -1e9;
                            maxi = max(maxi,value);

                        }
                    }
                 temp[col1][col2] = maxi;    
                }
            }
          next = temp;
        }
        return next[0][m-1];
    }
};
```
