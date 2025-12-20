# Recursion

```c++
class Solution {
public:
    int max_point(vector<int>& nums,int ind){
        if(ind == 0)return nums[0];
        if(ind < 0)return 0;

        int pick = nums[ind] + max_point(nums,ind-2);
        int notpick = 0 + max_point(nums,ind-1);
        return max(pick,notpick);
    }
    int rob(vector<int>& nums) {
        int n = nums.size();
        return max_point(nums,n-1);
    }
};
```
# Memoization
```c++
class Solution {
public:
    int max_point(vector<int>& nums,int ind,vector<int>&dp){
        if(ind == 0)return dp[0] = nums[0];
        if(ind < 0)return 0;
        if(dp[ind] != -1)return dp[ind];
        int pick = nums[ind] + max_point(nums,ind-2,dp);
        int notpick = 0 + max_point(nums,ind-1,dp);
        return dp[ind] = max(pick,notpick);
    }
    int rob(vector<int>& nums) {
        int n = nums.size();
        vector<int>dp(n,-1);
        return max_point(nums,n-1,dp);
    }
};
```
# Tabulation

```c++
class Solution {
public:
    int rob(vector<int>& nums) {
        int n = nums.size();
        vector<int>dp(n);
        dp[0] = nums[0];
        for(int i=1;i<n;i++){
           int pick = nums[i];
           if(i>1)pick += dp[i-2];
           int notpick = dp[i-1];
           dp[i] = max(pick,notpick);
       }
        return dp[n-1];
    }
};
```