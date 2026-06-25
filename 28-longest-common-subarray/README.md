# [Problem Link](https://leetcode.com/problems/maximum-length-of-repeated-subarray/)

# Tabulation
```c++
class Solution {
public:
    int findLength(vector<int>& nums1, vector<int>& nums2) {
        int n = nums1.size();
        int m = nums2.size();
        int max_len = 0;
        vector<vector<int>>dp(n+1,vector<int>(m+1,0));
        for(int idx1=1;idx1<n+1;idx1++){
            for(int idx2=1;idx2<m+1;idx2++){
                 if(nums1[idx1-1] == nums2[idx2-1])
                 {
                    dp[idx1][idx2] = 1+dp[idx1-1][idx2-1];
                    max_len = max(dp[idx1][idx2],max_len);
                 }
            }
		}
        return max_len;
    }
};
```

# Space Optimization
```c++
class Solution {
public:
    int findLength(vector<int>& nums1, vector<int>& nums2) {
        int n = nums1.size();
        int m = nums2.size();
        int max_len = 0;
        vector<int>prev(m+1,0);
        vector<int>temp = prev;
        for(int idx1=1;idx1<n+1;idx1++){
            for(int idx2=1;idx2<m+1;idx2++){
                 if(nums1[idx1-1] == nums2[idx2-1])
                 {
                    temp[idx2] = 1+prev[idx2-1];
                    max_len = max(temp[idx2],max_len);
                 }else temp[idx2] = 0;
            }
            prev = temp;
		}
        return max_len;
    }
};
```