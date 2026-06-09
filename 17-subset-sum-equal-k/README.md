# [Problem Link](https://www.naukri.com/code360/problems/count-subsets-with-sum-k_3952532?leftPanelTabValue=PROBLEM)

# Recursion + Memoization

```c++
int mod = 1e9+7;
int count(int ind,int tar,vector<int> &arr,vector<vector<int>>& dp){
	if(ind == 0  && tar == 0 && arr[0] == 0){
		return 2;
	}else if(ind == 0 && tar == 0)return 1;
	else if(ind == 0 && arr[0] == tar)return 1;
	else if(ind == 0 && arr[0] != tar)return 0;
	if(dp[ind][tar] != -1)return dp[ind][tar];
	int take = 0;
	if(arr[ind] <= tar){
		take = count(ind-1,tar-arr[ind],arr,dp);
	}
	int notTake = count(ind-1,tar,arr,dp);

	return dp[ind][tar] = (take + notTake)%mod;
}
int findWays(vector<int>& arr, int k)
{
	// Write your code here.
	int n = arr.size();
	vector<vector<int>>dp(n,vector<int>(k+1,-1));
	return count(n-1,k,arr,dp);

}

```

# Tabulation

```c++
int mod = 1e9+7;

int findWays(vector<int>& arr, int k)
{
	// Write your code here.
	int n = arr.size();
	vector<vector<int>>dp(n,vector<int>(k+1,0));
	if(arr[0] == 0){
		dp[0][0] =  2;
	}else dp[0][0] = 1;
	if(arr[0] <= k && arr[0]!=0)dp[0][arr[0]] = 1;

	for(int ind=1;ind<n;ind++){
		for(int tar=0;tar<=k;tar++){
			int take = 0;
			if(arr[ind] <= tar){
				take = dp[ind-1][tar-arr[ind]];
			}
			int notTake = dp[ind-1][tar];

		   dp[ind][tar] = (take + notTake)%mod;
		}
	}
	return dp[n-1][k];
}

```

# Space Optimization

```c++

int mod = 1e9+7;

int findWays(vector<int>& arr, int k)
{
	// Write your code here.
	int n = arr.size();
	vector<int>prev(k+1,0);
	vector<int>temp = prev;

	if(arr[0] == 0){
		prev[0] =  2;
	}else prev[0] = 1;
	if(arr[0] <= k && arr[0]!=0)prev[arr[0]] = 1;

	for(int ind=1;ind<n;ind++){
		for(int tar=0;tar<=k;tar++){
			int take = 0;
			if(arr[ind] <= tar){
				take = prev[tar-arr[ind]];
			}
			int notTake = prev[tar];

		   temp[tar] = (take + notTake)%mod;
		}
		prev = temp;
	}
	return prev[k];
}

```