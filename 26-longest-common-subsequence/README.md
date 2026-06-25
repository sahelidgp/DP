# [Problem Link](https://leetcode.com/problems/longest-common-subsequence/description/)

# Recursion + Memoization
# Tc: O(nxm)
# Sc: O(nxm)+O(n+m)
```c++
class Solution {
public:
    int f(int idx1,int idx2,string &text1,string &text2,vector<vector<int>>&dp){
        if(idx1 < 0 || idx2 < 0)return 0;
        if(dp[idx1][idx2] != -1)return dp[idx1][idx2];
        if(text1[idx1] == text2[idx2])return dp[idx1][idx2] = 1+f(idx1-1,idx2-1,text1,text2,dp);

        return dp[idx1][idx2] = max(f(idx1-1,idx2,text1,text2,dp),f(idx1,idx2-1,text1,text2,dp));
    }
    int longestCommonSubsequence(string text1, string text2) {
        int len1 = text1.size();
        int len2 = text2.size();
        vector<vector<int>>dp(len1,vector<int>(len2,-1));
        return f(len1-1,len2-1,text1,text2,dp);
    }
};
```

# Tabulation

shifting of index as the recursion base case is going to negative
```c++
class Solution {
public:
    int longestCommonSubsequence(string text1, string text2) {
        int len1 = text1.size();
        int len2 = text2.size();
        vector<vector<int>>dp(len1+1,vector<int>(len2+1,0));
        for(int idx1=1;idx1<len1+1;idx1++){
            for(int idx2=1;idx2<len2+1;idx2++){
                 if(text1[idx1-1] == text2[idx2-1])dp[idx1][idx2] = 1+dp[idx1-1][idx2-1];
                 else dp[idx1][idx2] = max(dp[idx1-1][idx2],dp[idx1][idx2-1]);
                 
            }
        }
        return dp[len1][len2];
    }
};
```
# Space Optimization

```c++
class Solution {
public:
    int longestCommonSubsequence(string text1, string text2) {
        int len1 = text1.size();
        int len2 = text2.size();
        vector<int>prev(len2+1,0);
        vector<int>temp = prev;
        for(int idx1=1;idx1<len1+1;idx1++){
            for(int idx2=1;idx2<len2+1;idx2++){
                 if(text1[idx1-1] == text2[idx2-1])temp[idx2] = 1+prev[idx2-1];
                 else temp[idx2] = max(prev[idx2],temp[idx2-1]);
                 
            }
            prev = temp;
        }
        return prev[len2];
    }
};
```