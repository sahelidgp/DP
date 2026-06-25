# [Problem link](https://leetcode.com/problems/shortest-common-supersequence/description/)

# Code❤️
```c++
class Solution {
public:
    string shortestCommonSupersequence(string s1, string s2) {
        int n = s1.length();
        int m = s2.length();
        vector<vector<int>>dp(n+1,vector<int>(m+1,0));
        for(int idx1=1;idx1<n+1;idx1++){
            for(int idx2=1;idx2<m+1;idx2++){
                 if(s1[idx1-1] == s2[idx2-1])dp[idx1][idx2] = 1+dp[idx1-1][idx2-1];
                 else dp[idx1][idx2] = max(dp[idx1-1][idx2],dp[idx1][idx2-1]);    
            }
		}
		int i = n;
		int j = m;
		string ans;
		while(i > 0 && j>0){
			if(s1[i-1] == s2[j-1]){
				ans = s1[i-1]+ans;
				i--;
				j--;
			}
			else if(dp[i-1][j] > dp[i][j-1]){
                ans = s1[i-1]+ans;
				i--;
			}
			else {
                ans = s2[j-1]+ans;
                j--;
            }
		}
        while(i){
            ans = s1[i-1]+ans;
            i--;
        }
        while(j){
            ans = s2[j-1]+ans;
                j--;
        }
	 return ans;
    }
};
```