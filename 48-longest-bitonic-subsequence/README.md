# [Problem Link](https://www.geeksforgeeks.org/problems/longest-bitonic-subsequence0824/1)

# Code❤️
```c++
class Solution {
  public:
    int longestBitonicSequence(int n, vector<int> &nums) {
        // code here
        vector<int>dp1(n,1);
        vector<int>dp2(n,1);
        for(int ind=1;ind<n;ind++){
            for(int prev = 0;prev<ind;prev++){
                if(nums[prev]<nums[ind])dp1[ind] = max(dp1[ind],1+dp1[prev]);
            }
        }
        for(int ind=n-1;ind>=0;ind--){
            for(int prev = n-1;prev>ind;prev--){
                if(nums[prev]<nums[ind])dp2[ind] = max(dp2[ind],1+dp2[prev]);
            }
        }
        
        int max_biton_len = 0;
        for(int i=0;i<n;i++){
            if(dp1[i] > 1 && dp2[i] > 1)
            max_biton_len = max(max_biton_len,dp1[i]+dp2[i]-1);
        }
        return max_biton_len;
    }
};
mkd
```