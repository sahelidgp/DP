# [Problem Link]()

# Recursion+Memo

```c++
class Solution {
  public:
    int f(int ind,int len,vector<int> &price,vector<vector<int>>& dp){
        if(len == 0)return 0;
        if(ind == 0)return price[ind]*len;
        
        if(dp[ind][len] != -1)return dp[ind][len];
        
        int take = 0;
        if(len >= ind+1)
        take = price[ind] + f(ind,len-(ind+1),price,dp);
        int notTake = f(ind-1,len,price,dp);
        return dp[ind][len] = max(take,notTake);
        
    }
    int cutRod(vector<int> &price) {
        // code here
        int n = price.size();
        vector<vector<int>>dp(n,vector<int>(n+1,-1));
        
        return f(n-1,n,price,dp);
    }
};
```

# Tabulation
```c++
class Solution {
  public:
    int cutRod(vector<int> &price) {
        // code here
        int n = price.size();
        vector<vector<int>>dp(n,vector<int>(n+1,0));
        
        for(int ind = 0;ind<n;ind++){
            for(int len = 0;len<n+1;len++){
                if(len == 0)continue;
                if(ind == 0)dp[ind][len] = price[ind]*len;
                else{ 
                int take = 0;
                if(len >= ind+1)
                take = price[ind] + dp[ind][len-(ind+1)];
                int notTake = dp[ind-1][len];
                dp[ind][len] = max(take,notTake);
                }
            }
        }
        
        return dp[n-1][n];
    }
};
```

# Space Optimized

```c++
class Solution {
  public:
    int cutRod(vector<int> &price) {
        // code here
        int n = price.size();
        vector<int>prev(n+1,0);
        for(int len=0;len<n+1;len++){
            prev[len] = price[0]*len;
        }
        vector<int>temp = prev;
        for(int ind = 1;ind<n;ind++){
            for(int len = 0;len<n+1;len++){
                if(len == 0)continue;
                else{ 
                int take = 0;
                if(len >= ind+1)
                take = price[ind] + temp[len-(ind+1)];
                int notTake = prev[len];
                temp[len] = max(take,notTake);
                }
            }
            prev = temp;
        }
        
        return prev[n];
    }
};
```