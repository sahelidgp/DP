# [Problem Link](https://www.naukri.com/code360/problems/unbounded-knapsack_1215029?resumeRedirection=true&leftPanelTabValue=PROBLEM)

# Recursion + Memoization
```c++

int f(int idx,int cap,vector<int>& profit, vector<int>& weight,vector<vector<int>>& dp){
    if(cap <= 0)return 0;
    if(idx == 0){
        if(cap < weight[idx])return 0;
        else if(cap%weight[0] == 0)return profit[0]*(cap/weight[idx]);
        else return 0;
    }
    if(dp[idx][cap] != -1)return dp[idx][cap];
    int take = 0;
    if(weight[idx] <= cap)take = profit[idx] + f(idx,cap-weight[idx],profit,weight,dp);
    int notTake = f(idx-1,cap,profit,weight,dp);

    return dp[idx][cap] =  max(take,notTake);
}
int unboundedKnapsack(int n, int w, vector<int> &profit, vector<int> &weight){
    // Write Your Code Here.
    vector<vector<int>>dp(n,vector<int>(w+1,-1));
    return f(n-1,w,profit,weight,dp);
}
```

# Tabulation

```c++

int unboundedKnapsack(int n, int w, vector<int> &profit, vector<int> &weight){
    // Write Your Code Here.
    vector<vector<int>>dp(n,vector<int>(w+1,0));
    //base case
    for(int cap = 1;cap<= w;cap++){
        if(cap%weight[0] == 0)dp[0][cap] =  profit[0]*(cap/weight[0]);
    }
    for(int item = 1;item < n;item ++){
        for(int cap = 0;cap <= w;cap++){
            int take = 0;
            if(weight[item] <= cap)take = profit[item] + dp[item][cap-weight[item]];
            int notTake = dp[item-1][cap];

         dp[item][cap] =  max(take,notTake);
        }
    }
    return dp[n-1][w];
}

```

# Space Optimization

```c++

int unboundedKnapsack(int n, int w, vector<int> &profit, vector<int> &weight){
    // Write Your Code Here.
    vector<int>prev(w+1,0);
    //base case
    for(int cap = 1;cap<= w;cap++){
        if(cap%weight[0] == 0)prev[cap] =  profit[0]*(cap/weight[0]);
    }
    vector<int>temp = prev;
    for(int item = 1;item < n;item ++){
        for(int cap = 0;cap <= w;cap++){
            int take = 0;
            if(weight[item] <= cap)take = profit[item] + temp[cap-weight[item]];
            int notTake = temp[cap];

         temp[cap] =  max(take,notTake);
        }
        prev = temp;
    }
    return prev[w];
}
```
