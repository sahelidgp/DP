# [Problem Link](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)

# Code
```c++
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int max_profit = 0;
        int n = prices.size();
        int min_price = prices[0];
        for(int i=1;i<n;i++){
            int curr_profit = prices[i]-min_price;
            max_profit = max(max_profit,curr_profit);
            min_price = min(min_price,prices[i]);
        }
        return max_profit;
    }
};
```