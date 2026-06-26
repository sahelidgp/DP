# [Problem Link](https://leetcode.com/problems/edit-distance/)

# Code❤️
# Recursion+memo

```c++
class Solution {
public:

    int count(int i,int j,string & s,string & t,vector<vector<int>>& dp){
        //base case
        if(i<0)return j+1;
        if(j<0)return i+1;

        if(dp[i][j]!=-1)return dp[i][j];
        //match case
        if(s[i] == t[j])return dp[i][j] = count(i-1,j-1,s,t,dp);
        //not match case
        int deletion = 1 + count(i-1,j,s,t,dp);
        int insertion = 1 + count(i,j-1,s,t,dp);
        int replacement = 1 + count(i-1,j-1,s,t,dp);

        return dp[i][j] = min({deletion,insertion,replacement});

    }
    int minDistance(string word1, string word2) {
        int n = word1.length();
        int m = word2.length();
        vector<vector<int>>dp(n,vector<int>(m,-1));
        return count(n-1,m-1,word1,word2,dp);
    }
};
```
# Tabulation
```c++
class Solution {
public:

    int minDistance(string word1, string word2) {
        int n = word1.length();
        int m = word2.length();
        vector<vector<int>>dp(n+1,vector<int>(m+1,0));

        //base case
        for(int i=1;i<n+1;i++){
            dp[i][0] = i;
        }
        for(int j=1;j<m+1;j++){
            dp[0][j] = j;
        }
        for(int i=1;i<n+1;i++){
            for(int j=1;j<m+1;j++){
                 if(word1[i-1] == word2[j-1]) dp[i][j] = dp[i-1][j-1];
        //not match case
                else{
                    
                int deletion = 1 + dp[i-1][j];
                int insertion = 1 + dp[i][j-1];
                int replacement = 1 + dp[i-1][j-1];

                dp[i][j] = min({deletion,insertion,replacement});
                }
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

    int minDistance(string word1, string word2) {
        int n = word1.length();
        int m = word2.length();
        vector<int>prev(m+1,0);
        
        //base case
        for(int j=0;j<m+1;j++){
            prev[j] = j;
        }
        vector<int>temp = prev;
        for(int i=1;i<n+1;i++){
            temp[0] = i;
            for(int j=1;j<m+1;j++){
                 if(word1[i-1] == word2[j-1]) temp[j] = prev[j-1];
        //not match case
                else{
                    
                int deletion = 1 + prev[j];
                int insertion = 1 + temp[j-1];
                int replacement = 1 + prev[j-1];

                temp[j] = min({deletion,insertion,replacement});
                }
            }
         prev = temp;
        }
        return prev[m];
    }
};
```