# [Problem Link](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/description/)
# Greedy approach
```c++
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int n = prices.size();
        int profit = 0;
        for(int i=1;i<n;i++){
            if(prices[i]>prices[i-1])profit += prices[i]-prices[i-1];
        }
        return profit;
    }
};
```

# Dp Approach
# memoization  
time complexity = O(nx2) + O(n)
```c++
class Solution {
public:
    int f(int ind,int buy,vector<int>& prices,vector<vector<int>> &dp){
        int n = prices.size();
        if(ind == n)return 0;
        if(dp[ind][buy] != -1)return dp[ind][buy];
        int profit = 0;
        if(buy){
            profit = max(-prices[ind]+f(ind+1,0,prices,dp),f(ind+1,1,prices,dp));
        }else{
            profit = max(prices[ind]+f(ind+1,1,prices,dp),f(ind+1,0,prices,dp));
        }
        return dp[ind][buy] =  profit;
    }
    int maxProfit(vector<int>& prices) {
        int n = prices.size();

        vector<vector<int>>dp(n,vector<int>(2,-1));
        return f(0,1,prices,dp);
    }
};
```

# Tabulation

```c++
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int n = prices.size();

        vector<vector<int>>dp(n+1,vector<int>(2,0));

       for(int ind=n-1;ind>=0;ind--){
         int profit = 0;
         for(int buy=0;buy<2;buy++){
        if(buy){
            profit = max(-prices[ind]+dp[ind+1][0],dp[ind+1][1]);
        }else{
            profit = max(prices[ind]+dp[ind+1][1],dp[ind+1][0]);
        }
        dp[ind][buy] =  profit;
         }
       } 
    return dp[0][1];
    }
};
```
# Space Optimized
```c++
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int n = prices.size();

       vector<int>next(2,0);
        vector<int>temp(2,0);
       for(int ind=n-1;ind>=0;ind--){
         int profit = 0;
         for(int buy=0;buy<2;buy++){
        if(buy){
            profit = max(-prices[ind]+next[0],next[1]);
        }else{
            profit = max(prices[ind]+next[1],next[0]);
        }
        temp[buy] =  profit;
         }
         next = temp;
       } 
    return next[1];
    }
};
```