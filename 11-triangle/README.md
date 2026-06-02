 # Triangle

Given a triangle array, return the minimum path sum from top to bottom.

For each step, you may move to an adjacent number of the row below. More formally, if you are on index i on the current row, you may move to either index i or index i + 1 on the next row.

 
```
Example 1:

Input: triangle = [[2],[3,4],[6,5,7],[4,1,8,3]]
Output: 11
Explanation: The triangle looks like:
   2
  3 4
 6 5 7
4 1 8 3
The minimum path sum from top to bottom is 2 + 3 + 5 + 1 = 11 (underlined above).
Example 2:

Input: triangle = [[-10]]
Output: -10
 

Constraints:

1 <= triangle.length <= 200
triangle[0].length == 1
triangle[i].length == triangle[i - 1].length + 1
-104 <= triangle[i][j] <= 104
 

Follow up: Could you do this using only O(n) extra space, where n is the total number of rows in the triangle?
```

# Recursion+Memoization
```c++
class Solution {
public:
    int sum_path(int row,int col,vector<vector<int>>& triangle,vector<vector<int>>& dp){
        int n = triangle.size();
        if(row == n-1)return triangle[row][col];
        if(dp[row][col] != 1e9)return dp[row][col];

        int diag = sum_path(row+1,col+1,triangle,dp);
        int down = sum_path(row+1,col,triangle,dp);

        return dp[row][col] = min(diag,down)+triangle[row][col];
    }
    int minimumTotal(vector<vector<int>>& triangle) {
        int n = triangle.size();
        vector<vector<int>>dp(n,vector<int>(n,1e9));
        return sum_path(0,0,triangle,dp);
    }
};
```
# Tabulation
```c++
class Solution {
public:
    int minimumTotal(vector<vector<int>>& triangle) {
        int n = triangle.size();
        vector<vector<int>>dp(n,vector<int>(n,1e9));
        int min_sum = 1e9;
        for(int row = 0;row < n;row++){
            for(int col = 0;col < triangle[row].size();col++){
                if(row == 0 && col == 0)dp[row][col] = triangle[row][col];
                else if(col == 0)dp[row][col] = dp[row-1][col]+triangle[row][col];
                else dp[row][col] = min(dp[row-1][col],dp[row-1][col-1])+triangle[row][col];
                if(row == n-1)min_sum = min(min_sum,dp[row][col]);
                
            }
        } 
        return min_sum;
    }
};
```
# Space Optimization

```c++
class Solution {
public:
    int minimumTotal(vector<vector<int>>& triangle) {
        int n = triangle.size();
        vector<int>prev(n,1e9);
        vector<int>temp(n,1e9);
        int min_sum = 1e9;
        for(int row = 0;row < n;row++){
            for(int col = 0;col < triangle[row].size();col++){
                if(row == 0 && col == 0)temp[col] = triangle[row][col];
                else if(col == 0)temp[col] = prev[col]+triangle[row][col];
                else temp[col] = min(prev[col],prev[col-1])+triangle[row][col];
                if(row == n-1)min_sum = min(min_sum,temp[col]);
                
            }
            prev = temp;
        } 
        return min_sum;
    }
};
```