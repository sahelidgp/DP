# [Problem Link](https://leetcode.com/problems/distinct-subsequences/description/)

# Code❤️

# Memo+recursion
```c++
class Solution {
public:
    int count(int i,int j,string &s,string &t,vector<vector<int>>& dp){
        //base case
        if(j < 0)return 1;
        if(i < 0)return 0;

        if(dp[i][j] != -1)return dp[i][j];
        //match case
        if(s[i] == t[j])return dp[i][j] = count(i-1,j-1,s,t,dp) + count(i-1,j,s,t,dp);
        //not match case
        return dp[i][j] = count(i-1,j,s,t,dp);
    }
    int numDistinct(string s, string t) {
        int n = s.length();
        int m = t.length();
        vector<vector<int>>dp(n,vector<int>(m,-1));
        return count(n-1,m-1,s,t,dp);
    }
};
```
# Tabulation
```c++
class Solution {
public:
    int numDistinct(string s, string t) {
        int n = s.length();
        int m = t.length();
        vector<vector<unsigned int>>dp(n+1,vector<unsigned int>(m+1,0));
        //base case 
        for(int i=0;i<n+1;i++){
            dp[i][0] = 1;
        }
        //explore
        for(int i=1;i<n+1;i++){
            for(int j=1;j<m+1;j++){
                 //match case
                if(s[i-1] == t[j-1]){
                    dp[i][j] = dp[i-1][j-1] + dp[i-1][j];
                }
                //not match case
                else dp[i][j] = dp[i-1][j];
            }
        }
        return dp[n][m];
    }
};
```
# Space Optimized
```c++
class Solution {
public:
    int numDistinct(string s, string t) {
        int n = s.length();
        int m = t.length();
        //base case
        vector<unsigned int>prev(m+1,0);
        prev[0] = 1;
        vector<unsigned int>temp = prev; 
        //explore
        for(int i=1;i<n+1;i++){
            for(int j=1;j<m+1;j++){
                 //match case
                if(s[i-1] == t[j-1]){
                    temp[j] = prev[j-1] + prev[j];
                }
                //not match case
                else temp[j] = prev[j];
            }
            prev = temp;
        }
        return temp[m];
    }
};
```