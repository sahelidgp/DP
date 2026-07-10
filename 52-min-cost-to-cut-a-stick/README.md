# [Problem Link](https://leetcode.com/problems/minimum-cost-to-cut-a-stick/description/)

# Recursion + memo
tc : O(sz^2 x sz)
sc : O(sz^2) + O(sz)
```c++
class Solution{
    public:
int solve(int i,int j,vector<int>&cuts,vector<vector<int>>&dp)
    {
        if(i>j)return 0;
        int mini=1e9;
        if(dp[i][j]!=-1)return dp[i][j];
        for(int ind=i;ind<=j;ind++)
        {
            int cost=cuts[j+1]-cuts[i-1]+solve(i,ind-1,cuts,dp)+solve(ind+1,j,cuts,dp);
            if(cost<mini)mini=cost;
        }
         return dp[i][j]=mini;
    }
    
    int minCost(int n, vector<int>& cuts) {
        int sz=cuts.size();
        cuts.push_back(n);
        cuts.insert(cuts.begin(),0);
        sort(cuts.begin(),cuts.end());
        vector<vector<int>>dp(sz+1,vector<int>(sz+1,-1));
        return solve(1,sz,cuts,dp);
        
    }
    };
```

# Tabulation

```c++
class Solution{
    public:
    int minCost(int n, vector<int>& cuts) {
        int sz=cuts.size();
        cuts.push_back(n);
        cuts.insert(cuts.begin(),0);
        sort(cuts.begin(),cuts.end());
        vector<vector<int>>dp(sz+2,vector<int>(sz+2,0));
        
        for(int i=sz;i>=1;i--){
            for(int j=1;j<=sz;j++){
                if(i>j)continue;
                int mini=1e9;
                for(int ind=i;ind<=j;ind++)
                    {
                     int cost=cuts[j+1]-cuts[i-1]+dp[i][ind-1]+ dp[ind+1][j];
                        if(cost<mini)mini=cost;
                    }
             dp[i][j]=mini;
            }
        }
        return dp[1][sz];
    }
    };
```