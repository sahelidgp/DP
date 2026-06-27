# [Problem Link](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-transaction-fee/description/)
# Code 🌸
# Space optimized

```c++
class Solution {
public:
    int maxProfit(vector<int>& prices, int fee) {
        int n = prices.size();

       vector<int>next(2,0);
        vector<int>temp(2,0);
       for(int ind=n-1;ind>=0;ind--){
         int profit = 0;
         for(int buy=0;buy<2;buy++){
        if(buy){
            profit = max(-prices[ind]+next[0],next[1]);
        }else{
            profit = max(prices[ind]-fee+next[1],next[0]);
        }
        temp[buy] =  profit;
         }
         next = temp;
       } 
    return next[1];
    }
};
```