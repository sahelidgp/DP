# [Problem Link](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iv/)

# Code❤️
# Recursion + memo 
```c++
class Solution {
public:
 int f(int ind,int transaction,int k,vector<int> &prices,vector<vector<int>> &dp){
        int n = prices.size();

        //base case
        if(ind == n || transaction == 2*k)return 0;
        if(dp[ind][transaction]!= -1)return dp[ind][transaction];
        int profit = 0;
        //can buy 
        if(transaction%2 == 0){
            //will buy
            int  profit1 = -prices[ind] + f(ind+1,transaction+1,k,prices,dp);
            //will not buy
            int profit2 = f(ind+1,transaction,k,prices,dp);
            profit = max(profit1,profit2);
        }else{//sell case
            //will sell
            int profit1 = prices[ind] + f(ind+1,transaction+1,k,prices,dp);
            //will not sell
            int profit2 = f(ind+1,transaction,k,prices,dp);
            profit = max(profit1,profit2);
        }
        return dp[ind][transaction] = profit;
    }
    int maxProfit(int k, vector<int>& prices) {
        int n = prices.size();
        vector<vector<int>>dp(n,vector<int>(2*k+1,-1));
        
        return  f(0,0,k,prices,dp);
    }
};

```
# Tabulation
```c++
class Solution {
public:
    int maxProfit(int k, vector<int>& prices) {
        int n = prices.size();
        vector<vector<int>>dp(n+1,vector<int>(2*k+1,0));
        for(int ind=n-1;ind>=0;ind--){
            for(int tran=0;tran<2*k;tran++){
                 int profit = 0;
                //can buy 
                if(tran%2 == 0){
                //will buy
                int  profit1 = -prices[ind] + dp[ind+1][tran+1];
                //will not buy
                int profit2 = dp[ind+1][tran];
                profit = max(profit1,profit2);
            }else{//sell case
                //will sell
                int profit1 = prices[ind] + dp[ind+1][tran+1];
                //will not sell
                int profit2 = dp[ind+1][tran];
                profit = max(profit1,profit2);
            }
           dp[ind][tran] = profit;
        }
    }
        
        return  dp[0][0];
    }
};
```
# Space Optimized

```c++
class Solution {
public:
    int maxProfit(int k, vector<int>& prices) {
        int n = prices.size();
        vector<int>after(2*k+1,0);
        
        for(int ind=n-1;ind>=0;ind--){
            vector<int>temp(2*k+1,0);
            for(int tran=0;tran<2*k;tran++){
                 int profit = 0;
                //can buy 
                if(tran%2 == 0){
                //will buy
                int  profit1 = -prices[ind] + after[tran+1];
                //will not buy
                int profit2 = after[tran];
                profit = max(profit1,profit2);
            }else{//sell case
                //will sell
                int profit1 = prices[ind] + after[tran+1];
                //will not sell
                int profit2 = after[tran];
                profit = max(profit1,profit2);
            }
           temp[tran] = profit;
        }
        after = temp;
    }
        
        return  after[0];
    }
};
```