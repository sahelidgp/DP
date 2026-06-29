# [Problem Link](https://leetcode.com/problems/number-of-longest-increasing-subsequence/description/)
# Code❤️
```c++
class Solution {
public:
    int findNumberOfLIS(vector<int>& nums) {
        int n = nums.size();
        vector<int>dp(n,1);
        vector<int>count(n,1);
        int maxi = 1;
        int max_ind = 0;
        for(int ind=1;ind<n;ind++){
            for(int prev = 0;prev<ind;prev++){
                if(nums[prev]<nums[ind] && dp[prev]+1 > dp[ind]){
                count[ind] = count[prev];
                dp[ind] = dp[prev]+1;
                }else if(nums[prev]<nums[ind] && dp[prev]+1 == dp[ind]){
                    count[ind] += count[prev];
                }
            }
            maxi = max(maxi, dp[ind]);
               
        }
        int total_count = 0;
        for(int i = 0; i < n; i++){
            if(dp[i] == maxi){
                total_count += count[i];
            }
        }
        
        return total_count;
      
    }
};
```