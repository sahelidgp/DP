# [Problem link](https://www.naukri.com/code360/problems/partitions-with-given-difference_3751628?leftPanelTabValue=PROBLEM)

```c++
#include <bits/stdc++.h> 
int mod = 1e9+7;
int countPartitions(int n, int d, vector<int> &arr) {
    // Write your code here.
    int totSum = accumulate(arr.begin(),arr.end(),0);
    if(totSum - d < 0 || (totSum - d) % 2 != 0) return 0;

    int sum = (totSum-d)/2;
    vector<int>prev(sum+1,0);
    //base case
    if(arr[0] == 0)prev[0] = 2;
    else prev[0] = 1;

    if(arr[0]>0 && arr[0]<=sum)prev[arr[0]] = 1;
    vector<int>temp = prev;

    int diffD_cnt = 0;
    for(int idx = 1;idx < n;idx++){
        for(int tar = 0;tar <= sum; tar++){
            int take = 0;
            if(arr[idx] <= tar)take = prev[tar-arr[idx]];

            int notTake = prev[tar];
            temp[tar] = (take + notTake)%mod;
        
        }
        prev = temp;
    }
return prev[sum];
}



```