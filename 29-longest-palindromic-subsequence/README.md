# [Problem Link](https://leetcode.com/problems/longest-palindromic-subsequence/)
 
 # Code
```c++
class Solution {
public:
    int longestPalindromeSubseq(string s) {
        int len1 = s.size();
        vector<int>prev(len1+1,0);
        string text1 = s;
        reverse(s.begin(),s.end());
        string text2 = s;
        vector<int>temp = prev;
        for(int idx1=1;idx1<len1+1;idx1++){
            for(int idx2=1;idx2<len1+1;idx2++){
                 if(text1[idx1-1] == text2[idx2-1])temp[idx2] = 1+prev[idx2-1];
                 else temp[idx2] = max(prev[idx2],temp[idx2-1]);
                 
            }
            prev = temp;
        }
        return prev[len1];
    }
};
```