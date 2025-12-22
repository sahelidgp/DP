
# 2D Dp

# Recursion

```c++
int f(int day,int last,vector<vector<int>>& points){
    //base case
    if(day == 0){
        int maxi = 0;
        for(int task=0;task<3;task++){
            if(task != last)
            maxi = max(maxi,points[day][task]);
        }
        return maxi;
    }
    int maxi = 0;
    for(int task=0;task<3;task++){
        if(task != last){
        int point = points[day][task] + f(day-1,task,points);
        maxi = max(maxi,point);
        }
    }
    return maxi;
}
int ninjaTraining(int n, vector<vector<int>> &points)
{
    // Write your code here.
    return f(n-1,3,points);
    
}

```
# Memoization
```c++
 
#include <bits/stdc++.h>
using namespace std;
int f(int day,int last,vector<vector<int>>& points,vector<vector<int>>& dp){
    //base case
    if(day == 0){
        int maxi = 0;
        for(int task=0;task<3;task++){
            if(task != last)
            maxi = max(maxi,points[day][task]);
        }
        return maxi;
    }
    if(dp[day][last] != -1)return dp[day][last];
    int maxi = 0;
    for(int task=0;task<3;task++){
        if(task != last){
            int point = points[day][task] +  f(day-1,task,points,dp);
            maxi = max(maxi,point);
        }
    }
    return dp[day][last] = maxi;
}
int ninjaTraining(int n, vector<vector<int>> &points)
{
    // Write your code here.
    vector<vector<int>>dp(n,vector<int>(4,-1));

    return f(n-1,3,points,dp);
    
}
int main()
{
    vector<vector<int>>points = {{2,1,3},{3,4,6},{10,1,6},{8,3,7}};
    cout<<ninjaTraining(4,points)<<endl;
    return 0;
}
```
# Tabulation
```c++

```