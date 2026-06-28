# [Problem Link](https://leetcode.com/problems/longest-string-chain/description/)

# Code❤️:)
```c++

//time complexity : O(n^2 x l) + O(nlogn)
//space complexity : O(n)
class Solution {
public:
   static bool cmp(const string &a, const string &b) {
        return a.length() < b.length();
    }
    bool compare(string &word1,string &word2){
        if(word2.length()-word1.length() != 1)return false;
        int i = 0;
        int j = 0;
        while(i<word1.length() && j<word2.length()){
            if(word1[i] == word2[j]){
                i++;
                j++;
            }
            else j++;
        }
       
       return i == word1.length();
    }
    int longestStrChain(vector<string>& words) {
        int n = words.size();
        sort(words.begin(), words.end(), cmp);
        vector<int>dp(n,1);
        int maxi = 1;
        for(int ind=1;ind<n;ind++){
            for(int prev = 0;prev<ind;prev++){
                if(compare(words[prev],words[ind]))dp[ind] = max(dp[ind],1+dp[prev]);
            }
            maxi = max(maxi,dp[ind]);
        }
        return maxi;
    }
};
```


