# [Problem Link](https://www.geeksforgeeks.org/problems/subset-sum-problem-1611555638/1)

# Recursion + Memoization
```c++
class Solution {
  public:
    bool f(int idx,int target,vector<int>& arr,vector<vector<int>>& dp){
        if(target == 0)return true;
        if(idx == 0)return arr[idx] == target;
        if(dp[idx][target]!=-1)return dp[idx][target];
        bool notTake = f(idx-1,target,arr,dp);
        bool take = false;
        if(arr[idx]<=target){
            take = f(idx-1,target-arr[idx],arr,dp);
        }
        return dp[idx][target] = take | notTake;
      }
    bool isSubsetSum(vector<int>& arr, int sum) {
        // code here
        int n = arr.size();
        vector<vector<int>>dp(n,vector<int>(sum+1,-1));
        return f(n-1,sum,arr,dp);
    }
};
```
# Tabulation

```c++
class Solution {
  public:
    
    bool isSubsetSum(vector<int>& arr, int sum) {
        // code here
        int n = arr.size();
        vector<vector<bool>>dp(n,vector<bool>(sum+1,false));
        
        for(int row = 0; row < n ;row++){
            dp[row][0] = true;
        }
        if(arr[0] <= sum)
        dp[0][arr[0]] = true;
        
        for(int ind = 1;ind <n;ind++){
            for(int target = 1;target<=sum;target++){
                bool notTake = dp[ind-1][target];
                
                bool take = false;
                if(arr[ind] <= target){
                    take = dp[ind-1][target-arr[ind]];
                    
                }
                dp[ind][target] = take | notTake;
             }
        }
        return dp[n-1][sum];
    }
};
```
# Space optimization

```c++
class Solution {
  public:
    
    bool isSubsetSum(vector<int>& arr, int sum) {
        // code here
        int n = arr.size();
        vector<bool>prev(sum+1,false);
        prev[0] = true;
        
        if(arr[0] <= sum)
        prev[arr[0]] = true;
        
        vector<bool>temp = prev;
        for(int ind = 1;ind<n;ind++){
                for(int target = 1;target<=sum;target++){
                bool notTake = prev[target];
                
                bool take = false;
                if(arr[ind] <= target){
                    take = prev[target-arr[ind]];
                    
                }
                temp[target] = take | notTake;
            }
            prev = temp;
        }
            
            
        return prev[sum];
    }
};
```