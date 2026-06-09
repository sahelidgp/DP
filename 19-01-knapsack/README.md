# [Problem Link](https://www.naukri.com/code360/problems/0-1-knapsack_920542?leftPanelTabValue=PROBLEM)

# Recursion + Memoization

```c++
#include <bits/stdc++.h> 

int f(int idx,int capacity,vector<int>& weight,vector<int>& value,vector<vector<int>>& dp){
	if(capacity <= 0)return 0;
	if(idx == 0 && weight[idx] <= capacity)return value[idx];
	else if(idx == 0 && weight[idx]>capacity)return 0;
	
	if(dp[idx][capacity] != -1)return dp[idx][capacity];

	int take = 0;
	if(weight[idx] <= capacity){
		take = value[idx] + f(idx-1,capacity-weight[idx],weight,value,dp);
	}
	int notTake = f(idx-1,capacity,weight,value,dp);

	return dp[idx][capacity] = max(take,notTake);
}
int knapsack(vector<int> weight, vector<int> value, int n, int maxWeight) 
{
	// Write your code here
	vector<vector<int>>dp(n,vector<int>(maxWeight+1,-1));
	return f(n-1,maxWeight,weight,value,dp);
}
```

# Tabulation

```c++
#include <bits/stdc++.h> 


int knapsack(vector<int> weight, vector<int> value, int n, int maxWeight) 
{
	// Write your code here
	vector<vector<int>>dp(n,vector<int>(maxWeight+1,0));

	//base case
	for(int wt = 1;wt <= maxWeight; wt ++){
		if(weight[0] <= wt)dp[0][wt] = value[0];
	}

	for(int item = 1;item <n; item ++){
		for(int cap = 1;cap<= maxWeight;cap ++){
			int take = 0;
			if(weight[item] <= cap)take = value[item] + dp[item-1][cap-weight[item]];
			int notTake = dp[item-1][cap];

			dp[item][cap] = max(take,notTake);
		}
	}
	return dp[n-1][maxWeight];
}
```

# Space Optimization

```c++
#include <bits/stdc++.h> 


int knapsack(vector<int> weight, vector<int> value, int n, int maxWeight) 
{
	// Write your code here
	vector<int>prev(maxWeight+1,0);

	//base case
	for(int wt = 1;wt <= maxWeight; wt ++){
		if(weight[0] <= wt)prev[wt] = value[0];
	}
	vector<int>temp = prev;
	for(int item = 1;item <n; item ++){
		for(int cap = 1;cap<= maxWeight;cap ++){
			int take = 0;
			if(weight[item] <= cap)take = value[item] + prev[cap-weight[item]];
			int notTake = prev[cap];

			temp[cap] = max(take,notTake);
		}
		prev = temp;
	}
	return prev[maxWeight];
}
```