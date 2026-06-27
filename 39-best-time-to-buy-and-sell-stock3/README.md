# [Problem Link](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iii/description/)

# Code❤️
# Recursion + memo
```c++
class Solution {
public:
//note : cap means one buy sell block
    int f(int ind,int buy,int cap,vector<int> &prices,vector<vector<vector<int>>> &dp){
        int n = prices.size();

        //base case
        if(ind == n)return 0;
        if(cap == 0)return 0;
        if(dp[ind][buy][cap]!=-1)return dp[ind][buy][cap];
        int profit = 0;
        //can buy 
        if(buy){
            //will buy
            int  profit1 = -prices[ind] + f(ind+1,0,cap,prices,dp);
            //will not buy
            int profit2 = f(ind+1,1,cap,prices,dp);
            profit = max(profit1,profit2);
        }else{//sell case
            //will sell
            int profit1 = prices[ind] + f(ind+1,1,cap-1,prices,dp);
            //will not sell
            int profit2 = f(ind+1,0,cap,prices,dp);
            profit = max(profit1,profit2);
        }
        return dp[ind][buy][cap] = profit;
    }
    int maxProfit(vector<int>& prices) {
        int n = prices.size();
        vector<vector<vector<int>>>dp(n,vector<vector<int>>(2,vector<int>(3,-1)));
        
        return  f(0,1,2,prices,dp);
    }
};
```
# Tabulation
```c++
class Solution {
public:
//note : cap means one buy sell block
    int maxProfit(vector<int>& prices) {
        int n = prices.size();
        vector<vector<vector<int>>>dp(n+1,vector<vector<int>>(2,vector<int>(3,0)));
        for(int ind=n-1;ind>=0;ind--){
            for(int buy=0;buy<=1;buy++){
                for(int cap=1;cap<=2;cap++){
                    int profit = 0;
                    //can buy 
                        if(buy){
                    //will buy
                     int  profit1 = -prices[ind] + dp[ind+1][0][cap];
                    //will not buy
                    int profit2 = dp[ind+1][1][cap];
                    profit = max(profit1,profit2);
                    }else{//sell case
                    //will sell
                    int profit1 = prices[ind] + dp[ind+1][1][cap-1];
                    //will not sell
                    int profit2 = dp[ind+1][0][cap];
                    profit = max(profit1,profit2);
                 }
                dp[ind][buy][cap] = profit;
                }
            }
        }
        return dp[0][1][2];
    }
};
```
# Space Optimized O(nx2x3)
```c++
class Solution {
public:
//note : cap means one buy sell block
    int maxProfit(vector<int>& prices) {
        int n = prices.size();
       vector<vector<int>>after(2,vector<int>(3,0));
       vector<vector<int>>temp(2,vector<int>(3,0));

        for(int ind=n-1;ind>=0;ind--){
            for(int buy=0;buy<=1;buy++){
                for(int cap=1;cap<=2;cap++){
                    int profit = 0;
                    //can buy 
                        if(buy){
                    //will buy
                     int  profit1 = -prices[ind] + after[0][cap];
                    //will not buy
                    int profit2 = after[1][cap];
                    profit = max(profit1,profit2);
                    }else{//sell case
                    //will sell
                    int profit1 = prices[ind] + after[1][cap-1];
                    //will not sell
                    int profit2 = after[0][cap];
                    profit = max(profit1,profit2);
                 }
                temp[buy][cap] = profit;
                }
                after = temp;
            }
        }
        return after[1][2];
    }
};

```
# nx4 method
```c++
class Solution {
public:
    int f(int ind,int transaction,vector<int> &prices,vector<vector<int>> &dp){
        int n = prices.size();

        //base case
        if(ind == n || transaction == 4)return 0;
        if(dp[ind][transaction]!= -1)return dp[ind][transaction];
        int profit = 0;
        //can buy 
        if(transaction%2 == 0){
            //will buy
            int  profit1 = -prices[ind] + f(ind+1,transaction+1,prices,dp);
            //will not buy
            int profit2 = f(ind+1,transaction,prices,dp);
            profit = max(profit1,profit2);
        }else{//sell case
            //will sell
            int profit1 = prices[ind] + f(ind+1,transaction+1,prices,dp);
            //will not sell
            int profit2 = f(ind+1,transaction,prices,dp);
            profit = max(profit1,profit2);
        }
        return dp[ind][transaction] = profit;
    }
    int maxProfit(vector<int>& prices) {
        int n = prices.size();
        vector<vector<int>>dp(n,vector<int>(4,-1));
        
        return  f(0,0,prices,dp);
    }
};
```