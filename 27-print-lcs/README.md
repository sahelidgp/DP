# [Problem Link](https://www.naukri.com/code360/problems/print-longest-common-subsequence_8416383?leftPanelTabValue=PROBLEM)

```c++

string findLCS(int n, int m,string &s1, string &s2){
	// Write your code here.
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
			else if(dp[i-1][j] >dp[i][j-1]){
				i--;
			}
			else j--;
		}
	return ans;
    }

```