# [Problem Link](https://www.geeksforgeeks.org/problems/minimum-sum-partition3317/1)

# Code

```c++
class Solution {
  public:
    int minDifference(vector<int>& arr) {
        // code here
        int n = arr.size();
        if(n == 1)return arr[0];
        int totSum = accumulate(arr.begin(),arr.end(),0);
        int sum = totSum/2;
        vector<vector<bool>>dp(n,vector<bool>(sum+1,false));
        
        //base case
        for(int idx = 0; idx < n;idx++){
            dp[idx][0] = true;
        }
        if(arr[0] <= sum)
        dp[0][arr[0]] = true;
        
        int min_diff = 1e9;
        for(int idx = 1;idx < n;idx ++){
            for(int target = 1;target <= sum;target ++){
                bool take = false;
                if(arr[idx] <= target)take = dp[idx-1][target-arr[idx]];
                
                bool notTake = dp[idx-1][target];
                
                dp[idx][target] = take | notTake;
                
                if(idx == n-1 && dp[idx][target]){
                    int subset1Sum = target;
                    int subset2Sum = totSum-target;
                    min_diff = min(subset2Sum-subset1Sum, min_diff);
                }
            }
        }
        return min_diff;
    }
};

```