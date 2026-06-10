# [Problem Link](https://leetcode.com/problems/coin-change/description/)

# Code
```c++
class Solution {
public:
    int coinChange(vector<int>& currency, int n) {
        int m = currency.size();
        vector<int> prev(n+1,0);
        
        //base case
        
        for(int tar = 1;tar<=n;tar++){
            if(tar%currency[0] == 0)prev[tar] = tar / currency[0];
            else prev[tar] = 1e9;
            
        }
        vector<int>temp = prev;
        for (int curr = 1;curr < m;curr++){
            for(int tar = 1;tar<= n;tar++){
                int take = 1e9;
                if(currency[curr] <= tar)take = 1 + temp[tar-currency[curr]];
                int notTake = prev[tar];
                
                 temp[tar] = min(take ,notTake);
            }
            prev = temp;
        }
        if(prev[n] == 1e9)return -1;
        return prev[n];
    }
};
```