# [Problem Link](https://www.geeksforgeeks.org/problems/-minimum-number-of-coins4426/1)

# Recursion+Memoization
```c++

class Solution {
  public:
    int count(int idx,int tar,vector<int> &currency,vector<vector<int>> &dp){
        //base case
        if (tar == 0) return 0;
        if(idx == 0){
            if(tar % currency[idx] == 0)return tar/currency[idx];
            else return 1e9;
        }
        if(dp[idx][tar] != -1)return dp[idx][tar];
        int take = 1e9;
        if(currency[idx] <= tar)take = 1 + count(idx,tar-currency[idx],currency,dp);
        int notTake = count(idx-1,tar,currency,dp);
        
        return dp[idx][tar] = min(take ,notTake);
    }
    int findMin(int n) {
        // code here
        vector<int> currency = {1,2,5,10};
        vector<vector<int>> dp(4,vector<int>(n+1,-1));
        return count(3,n,currency,dp);
    }
};
```
# Tabulation
```c++
class Solution {
  public:

    int findMin(int n) {
        // code here
        vector<int> currency = {1,2,5,10};
        vector<vector<int>> dp(4,vector<int>(n+1,0));
        
        //base case
        
        for(int tar = 1;tar<=n;tar++){
            if(tar%currency[0] == 0)dp[0][tar] = tar / currency[0];
            else dp[0][tar] = 1e9;
            
        }
        for (int curr = 1;curr < 4;curr++){
            for(int tar = 1;tar<= n;tar++){
                int take = 1e9;
                if(currency[curr] <= tar)take = 1 + dp[curr][tar-currency[curr]];
                int notTake = dp[curr-1][tar];
                
                 dp[curr][tar] = min(take ,notTake);
            }
        }
        return dp[3][n];
    }
};
```
# Space Optimization
```c++
class Solution {
  public:

    int findMin(int n) {
        // code here
        vector<int> currency = {1,2,5,10};
        vector<int> prev(n+1,0);
        
        //base case
        
        for(int tar = 1;tar<=n;tar++){
            if(tar%currency[0] == 0)prev[tar] = tar / currency[0];
            else prev[tar] = 1e9;
            
        }
        vector<int>temp = prev;
        for (int curr = 1;curr < 4;curr++){
            for(int tar = 1;tar<= n;tar++){
                int take = 1e9;
                if(currency[curr] <= tar)take = 1 + temp[tar-currency[curr]];
                int notTake = prev[tar];
                
                 temp[tar] = min(take ,notTake);
            }
            prev = temp;
        }
        return prev[n];
    }
};
```