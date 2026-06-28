# [Problem Link](https://www.geeksforgeeks.org/problems/printing-longest-increasing-subsequence/1)

# Code❤️

```c++
class Solution {
  public:
    vector<int> getLIS(vector<int>& nums) {
        // Code here
        int n = nums.size();
        vector<int>dp(n,1);
        //dp [i] signifies length of lis from 0 to i of nums
        vector<int>hash(n);
        int maxi = 1;
        int max_ind = 0;
        for(int ind=0;ind<n;ind++){
            hash[ind] = ind;
            for(int prev = 0;prev<ind;prev++){
                if(nums[prev]<nums[ind] && dp[prev]+1>dp[ind]){
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

			reverse(ans.begin(),ans.end());
        return ans;
    }
};
```