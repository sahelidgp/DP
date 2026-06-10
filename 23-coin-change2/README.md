# [Problem Link](https://leetcode.com/problems/coin-change-ii/description/)

# Code
```c++
class Solution {
public:
    int change(int n, vector<int>& currency) {
         int m = currency.size();
        vector<long long> prev(n+1,0);
        
        //base case
        prev[0] = 1;
        for(long long tar = 1;tar<=n;tar++){
            if(tar%currency[0] == 0)prev[tar] = 1;
            else prev[tar] = 0;
        }
        
        vector<long long>temp = prev;

        for (long long curr = 1;curr < m;curr++){
            for(long long tar = 1;tar<= n;tar++){
                int take = 0;
                if(currency[curr] <= tar)take = temp[tar-currency[curr]];
                long long notTake = prev[tar];
                
                 temp[tar] = take + notTake;
            }
            prev = temp;
        }
        return prev[n];
    }
};
```