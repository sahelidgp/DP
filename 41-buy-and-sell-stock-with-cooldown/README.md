# [Problem Link](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-cooldown/description/)
# Code❤️
# Recursion + memo
```c++

class Solution {
public:
int f(int ind,int buy,vector<int>& prices,vector<vector<int>> &dp){
        int n = prices.size();
        if(ind >= n)return 0;
        if(dp[ind][buy] != -1)return dp[ind][buy];
        int profit = 0;
        if(buy){
            profit = max(-prices[ind]+f(ind+1,0,prices,dp),f(ind+1,1,prices,dp));
        }else{
            profit = max(prices[ind]+f(ind+2,1,prices,dp),f(ind+1,0,prices,dp));
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

        vector<vector<int>>dp(n+2,vector<int>(2,0));
        for(int ind=n-1;ind>=0;ind--){
            for(int buy=0;buy<=1;buy++){
                int profit = 0;
                if(buy){
                 profit = max(-prices[ind]+dp[ind+1][0],dp[ind+1][1]);
                }else{
                profit = max(prices[ind]+dp[ind+2][1],dp[ind+1][0]);
                }
            dp[ind][buy] =  profit;
            }
        }
        return dp[0][1];
    }
};
```
# Space Optimization
```c++
class Solution {
public:
    int maxProfit(vector<int>& prices) {
         int n = prices.size();

        vector<int>after2(2,0);
        vector<int>after1(2,0);
        vector<int>temp(2,0);
        for(int ind=n-1;ind>=0;ind--){
            for(int buy=0;buy<=1;buy++){
                int profit = 0;
                if(buy){
                 profit = max(-prices[ind]+after1[0],after1[1]);
                }else{
                profit = max(prices[ind]+after2[1],after1[0]);
                }
            temp[buy] =  profit;
            }
            
            after2 = after1;
            after1 = temp;
            
        }
        return after1[1];
    }
};
```