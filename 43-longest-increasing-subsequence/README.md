# [Problem Link](https://leetcode.com/problems/longest-increasing-subsequence/description/)

# Code
# Recursion + Memo
```c++
class Solution {
public:
    int f(int ind,int prev_ind,vector<int>& nums,vector<vector<int>>& dp){
        if(ind == nums.size())return 0;
        if(dp[ind][prev_ind+1] != -1)return dp[ind][prev_ind+1];

        //can take case
        int len = 0;

        if(prev_ind == -1 || nums[ind]>nums[prev_ind])
        len = max(1 + f(ind+1,ind,nums,dp),f(ind+1,prev_ind,nums,dp));

        //not take case
        len = max(f(ind+1,prev_ind,nums,dp),len);
        
        return dp[ind][prev_ind+1] = len;
    }
    int lengthOfLIS(vector<int>& nums) {
        int n = nums.size();
        vector<vector<int>>dp(n,vector<int>(n+1,-1));
        return f(0,-1,nums,dp);
    }
};
```

# Tabulation
```c++

class Solution {
public:
    
    int lengthOfLIS(vector<int>& nums) {
        int n = nums.size();
        vector<vector<int>>dp(n+1,vector<int>(n+1,0));
        for(int ind = n-1;ind>=0;ind--){
            for(int prev_ind = ind-1;prev_ind>=-1;prev_ind--){
                 //can take case
                    int len = 0;

                    if(prev_ind == -1 || nums[ind]>nums[prev_ind])
                    len = max(1 + dp[ind+1][ind+1],dp[ind+1][prev_ind+1]);

                    //not take case
                    len = max(dp[ind+1][prev_ind+1],len);
        
         dp[ind][prev_ind+1] = len;
            }
        }
        return dp[0][0];
    }
};
```
# Space Optimized
```c++
class Solution {
public:
    
    int lengthOfLIS(vector<int>& nums) {
        int n = nums.size();
        vector<int>next(n+1,0);
        vector<int>curr(n+1,0);
        for(int ind = n-1;ind>=0;ind--){
            for(int prev_ind = ind-1;prev_ind>=-1;prev_ind--){
                 //can take case
                    int len = 0;

                    if(prev_ind == -1 || nums[ind]>nums[prev_ind])
                    len = max(1 + next[ind+1],next[prev_ind+1]);

                    //not take case
                    len = max(next[prev_ind+1],len);
        
         curr[prev_ind+1] = len;
            }
            next = curr;
        }
        return next[0];
    }
};
```

# algorithmic approach:

Tc: O(n^2)
Sc: O(n)
```c++
class Solution {
public:
    int lengthOfLIS(vector<int>& nums) {
        int n = nums.size();
        vector<int>dp(n,1);
        int maxi = 1;
        for(int ind=1;ind<n;ind++){
            for(int prev = 0;prev<ind;prev++){
                if(nums[prev]<nums[ind])dp[ind] = max(dp[ind],1+dp[prev]);
            }
            maxi = max(maxi,dp[ind]);
        }
        return maxi;
    }
};
```