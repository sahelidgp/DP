# [Problem Link](https://leetcode.com/problems/largest-divisible-subset/description/)

# Code❤️
```c++
class Solution {
public:
    vector<int> largestDivisibleSubset(vector<int>& nums) {
         int n = nums.size();
         sort(nums.begin(),nums.end());
        vector<int>dp(n,1);
        //dp [i] signifies length of lis from 0 to i of nums
        vector<int>hash(n);
        int maxi = 1;
        int max_ind = 0;
        for(int ind=1;ind<n;ind++){
            hash[ind] = ind;
            for(int prev = 0;prev<ind;prev++){
                if(nums[ind]%nums[prev] == 0 && dp[prev]+1>dp[ind]){
                    dp[ind] = max(dp[ind],1+dp[prev]);
                    hash[ind] = prev;
                }
            }
            if(dp[ind]>maxi){
                maxi = dp[ind];
                max_ind = ind;
            }
			
        }
        vector<int>ans;
            int i = max_ind;
            while(hash[i] != i){
				ans.push_back(nums[i]);
				i = hash[i];
			}
			ans.push_back(nums[i]);

			//reverse(ans.begin(),ans.end());
        return ans;
    }
};
```