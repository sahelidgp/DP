# [Problem Link](https://leetcode.com/problems/target-sum/)

# Code

```c++
class Solution {
public:
    int findTargetSumWays(vector<int>& arr, int target) {
        int n = arr.size();
        int totSum = accumulate(arr.begin(),arr.end(),0);
    if(totSum - target < 0 || (totSum - target) % 2 != 0) return 0;

    int sum = (totSum-target)/2;
    vector<int>prev(sum+1,0);
    //base case
    if(arr[0] == 0)prev[0] = 2;
    else prev[0] = 1;

    if(arr[0]>0 && arr[0]<=sum)prev[arr[0]] = 1;
    vector<int>temp = prev;

    for(int idx = 1;idx < n;idx++){
        for(int tar = 0;tar <= sum; tar++){
            int take = 0;
            if(arr[idx] <= tar)take = prev[tar-arr[idx]];

            int notTake = prev[tar];
            temp[tar] = (take + notTake);
        
        }
        prev = temp;
    }
return prev[sum];
    }
}; 
```