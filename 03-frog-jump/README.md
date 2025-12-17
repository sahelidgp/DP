# 🐸 Problem Statement: Min Energy Frog Jump
# Description:

# [Problem link](https://www.geeksforgeeks.org/problems/geek-jump/1)
A frog is trying to climb a staircase with n steps (indexed from 0 to n - 1). You’re given an array heights[] of length n, where heights[i] is the height of step i.

From step i, the frog can jump in two ways:

To step i + 1

Or to step i + 2 (if it exists)

Jumping from step i to step j (where j = i + 1 or i + 2) costs energy equal to abs(heights[i] - heights[j]) (the absolute difference in their heights).

Calculate and return the minimum total energy required for the frog to go from step 0 to step n - 1.


I became curious to find the optimal path 

here is the code
```c++
#include<bits/stdc++.h>
using namespace std;

  int find_cost(vector<int>&height,int idx,vector<int>&dp,vector<int>&parent){
      if(idx == 0)return dp[0] = 0;
      if(dp[idx] != -1)return dp[idx];
      int left = find_cost(height,idx-1,dp,parent)+abs(height[idx]-height[idx-1]);
      
      int right = 1e9;
      if(idx>1)
      right = find_cost(height,idx-2,dp,parent)+abs(height[idx]-height[idx-2]);
      int mini = min(left,right);
      if(left == mini)
      parent[idx] = (idx-1);
      else parent[idx] = (idx-2);
      return dp[idx] = mini;
  }
    int main(){
        vector<int> height = {30,10,60,10,60,50};
        // Code here
        int n = height.size();
        vector<int>dp(n,-1);
        vector<int> parent(n,-1);
        cout<< find_cost(height,n-1,dp,parent)<<endl;
        
        for(int i=0;i<n;i++){
            cout<<dp[i]<<" ";
        }
        cout<<endl;
        for(int i=0;i<parent.size();i++){
            cout<<parent[i]<<" ";
        }
        
        vector<int>path;
        int id = n-1;
        while(id != -1){
            path.push_back(id);
            id = parent[id];
        }
        reverse(path.begin(),path.end());
        cout<<endl;
        for(int i=0;i<path.size();i++){
            cout<<path[i]<<" ";
        }
        
        return 0;
    }
```
# if we want to find one optimal path
```c++
#include<bits/stdc++.h>
using namespace std;
int main(){
    vector<int>heights = {10,20,10,80,50,30,60,90};
    int n = heights.size();
    int k;
    cout<<"\nEnter the value of k : ";
    cin>>k;
    vector<int>dp(n);
    dp[0] = 0;
   vector<int>parent(n,-1);
   
    for(int i=1;i<n;i++){
         int mini = 1e9;
         int minj = -1;
        for(int j=1;j<=k;j++){
            if(i-j >= 0){
                int cost = dp[i-j]+abs(heights[i]-heights[i-j]);
                if(cost < mini){
                    mini = cost;
                    minj = i-j;
                }
            }
        }
        parent[i] = minj;
        dp[i] = mini;
    }
    for(int i=0;i<n;i++){
        cout<<dp[i]<<" ";
    }
    cout<<endl;
    
    for(int i=0;i<n;i++){
        cout<<parent[i]<<" ";
    }
    cout<<endl;
    vector<int>path;
    int id = n-1;
    while(id != -1){
        path.push_back(id);
        id = parent[id];
    }
    reverse(path.begin(),path.end());
    for(int i=0;i<path.size();i++){
        cout<<path[i]<<" ";
    }
    cout<<endl;
    cout<<endl<<dp[n-1];
}
```

# This is the code for finding all possible optimal path
```c++
#include <bits/stdc++.h>
using namespace std;

vector<vector<int>> allPaths;
vector<int> temp;

void dfs(int node, vector<vector<int>>& parent) {
    if (node == -1) {
        vector<int> path = temp;
        reverse(path.begin(), path.end());
        allPaths.push_back(path);
        return;
    }

    for (int p : parent[node]) {
        temp.push_back(node);
        dfs(p, parent);
        temp.pop_back();
    }
}

int main() {
    vector<int> heights = {10,20,10,80,50,30,60,90};
    int n = heights.size();
    int k;

    cout << "Enter k: ";
    cin >> k;

    vector<int> dp(n, 1e9);
    vector<vector<int>> parent(n);

    dp[0] = 0;
    parent[0].push_back(-1);

    for (int i = 1; i < n; i++) {
        for (int j = 1; j <= k; j++) {
            if (i - j >= 0) {
                int cost = dp[i - j] + abs(heights[i] - heights[i - j]);

                if (cost < dp[i]) {
                    dp[i] = cost;
                    parent[i].clear();
                    parent[i].push_back(i - j);
                }
                else if (cost == dp[i]) {
                    parent[i].push_back(i - j);
                }
            }
        }
    }

    // Print minimum energy
    cout << "\nMinimum energy = " << dp[n - 1] << "\n\n";

    // Backtrack all paths
    dfs(n - 1, parent);

    // Print all optimal paths
    cout << "All optimal paths:\n";
    for (auto &path : allPaths) {
        for (int x : path)
            cout << x << " ";
        cout << endl;
    }
}

```


# Recursion
```c++

int f(int ind,vector<int>& heights,vector<int>&dp){
    if(ind == 0)return 0;

    int left = f(ind-1,heights,dp) + abs(heights[ind]-heights[ind-1]);
    int right = INT_MAX;
    if(ind>1)
    right = f(ind-2,heights,dp) + abs(heights[ind]-heights[ind-2]);
    return  min(left,right);

}
int frogJump(int n,vector<int>& heights){
    vector<int> dp(n+1,-1);
    return f(n-1,heights,dp);
}

```
# Memoization[Top down]

```c++

int f(int ind,vector<int>& heights,vector<int>&dp){
    if(ind == 0)return 0;
    if(dp[ind] != -1) return dp[ind];

    int left = f(ind-1,heights,dp) + abs(heights[ind]-heights[ind-1]);
    int right = INT_MAX;
    if(ind>1)
    right = f(ind-2,heights,dp) + abs(heights[ind]-heights[ind-2]);
    return dp[ind] = min(left,right);

}
int frogJump(int n,vector<int>& heights){
    vector<int> dp(n,-1);
    return f(n-1,heights,dp);
}
```

# Tabulation[Bottom Up]


```c++

int frogJump(int n,vector<int>& heights){
    vector<int> dp(n,0);
    
    //base case
    dp[0] = 0;
    for(int i=1;i<n;i++){
        int fs = dp[i-1] + abs(heights[i]-heights[i-1]);
        int ss = INT_MAX;
        if(i>1)
        int rs = dp[i-2] + abs(heights[i]-heights[i-2]);

        dp[i] = min(fs,ss);
    }
    return dp[n-1];
}
```
# NOTE : 

if there is ind-1 and ind-2 then there will always be space optimization

# Space Optimization

```c++
int frogJump(int n,vector<int>& heights){
   
    int prev = 0;
    int prev2 = 0;
    int curr;
    for(int i=1;i<n;i++){
        int fs = prev + abs(heights[i]-heights[i-1]);
        int ss = INT_MAX;
        if(i>1)
         ss = prev2 + abs(heights[i]-heights[i-2]);

        curr = min(fs,ss);
        prev2 = prev;
        prev = curr;
    }
    return prev;
}


```
# Frog jump with K distances

A frog wants to climb a staircase with n steps. Given an integer array heights, where heights[i] contains the height of the ith step, and an integer k.



To jump from the ith step to the jth step, the frog requires abs(heights[i] - heights[j]) energy, where abs() denotes the absolute difference. The frog can jump from the ith step to any step in the range [i + 1, i + k], provided it exists. Return the minimum amount of energy required by the frog to go from the 0th step to the (n-1)th step.


Examples:
Input: heights = [10, 5, 20, 0, 15], k = 2

Output: 15

Explanation:

0th step -> 2nd step, cost = abs(10 - 20) = 10

2nd step -> 4th step, cost = abs(20 - 15) = 5

Total cost = 10 + 5 = 15.

Input: heights = [15, 4, 1, 14, 15], k = 3

Output: 2

Explanation:

0th step -> 3rd step, cost = abs(15 - 14) = 1

3rd step -> 4th step, cost = abs(14 - 15) = 1

Total cost = 1 + 1 = 2.


# ✅ Full Memoization Code:

```c++

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum cost to reach the end using at most 'k' jumps
int solveUtil(int ind, vector<int>& height, vector<int>& dp, int k) {
    // Base case: If we are at the beginning (index 0), no cost is needed.
    if (ind == 0) return 0;
    
    // If the result for this index has been previously calculated, return it.
    if (dp[ind] != -1) return dp[ind];
    
    int mmSteps = INT_MAX;
    
    // Loop to try all possible jumps from '1' to 'k'
    for (int j = 1; j <= k; j++) {
        // Ensure that we do not jump beyond the beginning of the array
        if (ind - j >= 0) {
            // Calculate the cost for this jump and update mmSteps with the minimum cost
            int jump = solveUtil(ind - j, height, dp, k) + abs(height[ind] - height[ind - j]);
            mmSteps = min(jump, mmSteps);
        }
    }
    
    // Store the minimum cost for this index in the dp array and return it.
    return dp[ind] = mmSteps;
}

// Function to find the minimum cost to reach the end of the array
int solve(int n, vector<int>& height, int k) {
    vector<int> dp(n, -1); // Initialize a memoization array to store calculated results
    return solveUtil(n - 1, height, dp, k); // Start the recursion from the last index
}

int main() {
    vector<int> height{30, 10, 60, 10, 60, 50};
    int n = height.size();
    int k = 2;
    vector<int> dp(n, -1); // Initialize a memoization array for the main function
    cout << solve(n, height, k) << endl; // Print the result of the solve function
    return 0;
}



```
# ✅Tabulation Code

```c++

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum cost to reach the end using at most 'k' jumps
int solveUtil(int n, vector<int>& height, vector<int>& dp, int k) {
    dp[0] = 0;

    // Loop through the array to fill in the dp array
    for (int i = 1; i < n; i++) {
        int mmSteps = INT_MAX;

        // Loop to try all possible jumps from '1' to 'k'
        for (int j = 1; j <= k; j++) {
            if (i - j >= 0) {
                int jump = dp[i - j] + abs(height[i] - height[i - j]);
                mmSteps = min(jump, mmSteps);
            }
        }
        dp[i] = mmSteps;
    }
    return dp[n - 1]; // The result is stored in the last element of dp
}

// Function to find the minimum cost to reach the end of the array
int solve(int n, vector<int>& height, int k) {
    vector<int> dp(n, -1); // Initialize a memoization array to store calculated results
    return solveUtil(n, height, dp, k);
}

int main() {
    vector<int> height{30, 10, 60, 10, 60, 50};
    int n = height.size();
    int k = 2;
    vector<int> dp(n, -1); // Initialize a memoization array for the main function
    cout << solve(n, height, k) << endl; // Print the result of the solve function
    return 0;
}


```
# ✅ Time & Space Complexity:

Time: O(n * k)

Space: O(n) for dp[] + O(n) recursion stack space.





# ✅ What is a Deque?
A deque (pronounced deck) stands for Double-Ended Queue.

It is a data structure that allows:

Insertion and Deletion from both ends — front and back — in O(1) time.

# 🔹 Properties of Deque:

Full Name	Double-Ended Queue
Operations	Push/Pop from Front & Back
Time Complexity	O(1) for all operations
Supports Random Access?	Yes (like vector)
STL in C++	#include <deque>

# 🔹 Visual Example:
Normal Queue (Single-ended):
text
Copy
Edit
Front  →  [ 1, 2, 3, 4 ]  →  Rear
Push at Rear, Pop at Front
Deque (Double-ended):

Front  ↔  [ 1, 2, 3, 4 ]  ↔  Rear
Push/Pop from Both Ends
# 🔹 Common Deque Functions in C++:
Operation	Purpose
dq.push_back(x)	Insert at the back
dq.push_front(x)	Insert at the front
dq.pop_back()	Remove from the back
dq.pop_front()	Remove from the front
dq.front()	Access front element
dq.back()	Access back element
dq.size()	Get current size

# 🔹 When Do We Use a Deque?
Sliding Window Problems

Monotonic Queue Problems

When we need fast insertions/removals from both ends.

When solving optimized DP problems with limited history

# ✅ Key Advantages:
Works like both a stack and a queue.

Very fast → O(1) push/pop from both ends.

C++ STL deque is highly optimized.

# ✅ Sliding Window Idea:
In standard DP:

dp[i] = min(dp[i - 1], dp[i - 2], ..., dp[i - k]) + cost
You need to look back at the last k elements.

👉 Instead of storing the entire dp[] array, you can store only the last k elements using a sliding window (queue or deque).

# 🚀 Optimized C++ Code (Sliding Window)
```c++
#include <bits/stdc++.h>
using namespace std;

class Solution {
public:
    int frogJump(vector<int>& heights, int k) {
        int n = heights.size();

        deque<pair<int, int>> window; // {index, dp value}
        window.push_back({0, 0}); // Start at stair 0 with 0 cost

        for (int i = 1; i < n; i++) {
            int minCost = INT_MAX;

            // Check all previous positions within the window
            for (auto& p : window) {
                minCost = min(minCost, p.second + abs(heights[i] - heights[p.first]));
            }

            // Push current stair into the window
            window.push_back({i, minCost});

            // Keep only the last k elements in the window
            if (window.size() > k)
                window.pop_front();
        }

        // The last element in the window is the final answer
        return window.back().second;
    }
};

```
# ✅ Explanation:
We store only the last k computed values in the window.

For each step, we compute the minimum cost using the window.

After computing, we push the current step into the window.

If the window size exceeds k, we pop the oldest element to keep only k elements.

# ✅ Complexity:
Time Complexity: O(n * k) → each step checks up to k previous steps.

Space Complexity: O(k) → we only store k previous results instead of n.

