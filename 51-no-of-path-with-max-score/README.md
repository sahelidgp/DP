#   [Problem Link](https://leetcode.com/problems/number-of-paths-with-max-score/description/)
# code
```c++
class Solution {
public:
int mod = 1e9 + 7;
    pair<int,int> solve(int r,int c,vector<string>& board,vector<vector<pair<int, int>>> &dp){
        if(r == 0 && c == 0)return {0,1};
        if(r<0 || c<0 || board[r][c] == 'X')return {-1,0};
        if (dp[r][c].second != -1) return dp[r][c];
        int val = (board[r][c] == 'S')?0:board[r][c]-'0';

        pair<int,int>up = solve(r-1,c,board,dp);
        pair<int,int>left = solve(r,c-1,board,dp);
        pair<int,int>diag = solve(r-1,c-1,board,dp);

        int max_sum = -1;
        int ways = 0;

        auto update = [&](pair<int,int> p){
            if(p.first>max_sum){
                max_sum = p.first;
                ways = p.second;
            }else if(p.first != -1 && p.first == max_sum){
                ways = (ways+p.second)%mod;
            }
        };
        update(up);
        update(left);
        update(diag);

        if(max_sum == -1)return dp[r][c] = {-1,0};
        return dp[r][c] = {max_sum+val,ways};

    }
    vector<int> pathsWithMaxScore(vector<string>& board) {
        int n = board.size();
        int m = board[0].size();
        vector<vector<pair<int, int>>> dp(n, vector<pair<int, int>>(m, {-1, -1}));
        pair<int, int> res = solve(n - 1, m - 1, board,dp);
       if (res.first == -1) return {0, 0};
        
        return {res.first, res.second};
    }
};
```