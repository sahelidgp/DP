# [Problem Link](https://leetcode.com/problems/edit-distance/description/)
# Code❤️
# Recursion+memo
```c++
class Solution {
public:
    bool f(int i,int j, string &s,string &p,vector<vector<int>> &dp){
        //base case 
        // if both gets exhausted
        if(i<0 && j<0)return true;
        //if s gets exhausted
        if(i<0)
        {
            while(j>=0){
                if(p[j]!='*')return false;
                else j--;
            }
            return true;
        }
        //if p gets exhausted 
        if(j<0)return false;
        if(dp[i][j] != -1)return dp[i][j];
         //exploration
         //match case
         if(s[i] == p[j] || p[j] == '?')return dp[i][j] = f(i-1,j-1,s,p,dp);
         //not match case
         if(p[j] == '*')return dp[i][j] = f(i-1,j,s,p,dp) | f(i,j-1,s,p,dp);
         return dp[i][j] = false;
    }
    
    bool isMatch(string s, string p) {
        int n = s.length();
        int m = p.length();
        vector<vector<int>>dp(n,vector<int>(m,-1));
        return f(n-1,m-1,s,p,dp);
    }
};
```
# Tabulation
```c++
class Solution {
public:
    bool isMatch(string s, string p) {
        int n = s.length();
        int m = p.length();
        vector<vector<bool>> dp(n + 1, vector<bool>(m + 1, false));
        dp[0][0] = true;
        //base case
        for(int j=1;j<m+1;j++){
            if(p[j-1] == '*')dp[0][j] = true;
            else break;
        }
        //exploration
        for(int i=1;i<n+1;i++){
            for(int j=1;j<m+1;j++){
                 // match case
                if (s[i-1] == p[j-1] || p[j-1] == '?')
                    dp[i][j] = dp[i - 1][j - 1];
                // not match case
                if (p[j-1] == '*')
                    dp[i][j] = dp[i - 1][j] | dp[i][ j - 1];
            }
        }
        return dp[n][m];
    }
};
```
# Space Optimization
```c++
class Solution {
public:
    bool isMatch(string s, string p) {
        int n = s.length();
        int m = p.length();
       vector<bool>prev(m + 1, false);
        prev[0] = true;
        //base case
        for(int j=1;j<m+1;j++){
            if(p[j-1] == '*')prev[j] = true;
            else break;
        }
        vector<bool>temp(m + 1, false);
        //exploration
        for(int i=1;i<n+1;i++){
            temp[0] = false;
            for(int j=1;j<m+1;j++){
                 // match case
                if (s[i-1] == p[j-1] || p[j-1] == '?')
                    temp[j] = prev[j - 1];
                // not match case
                else if (p[j-1] == '*')
                    temp[j] = prev[j] | temp[j - 1];
                else temp[j] = false;
            }
            prev = temp;
        }
        return prev[m];
    }
};
```

