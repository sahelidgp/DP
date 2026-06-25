# [Problem Link](https://leetcode.com/problems/minimum-insertion-steps-to-make-a-string-palindrome/description/)

# Code (Space Optimized)
```c++
class Solution {
public:
    int minInsertions(string s) {
        int n = s.size();
        vector<int>prev(n+1,0);
        string text1 = s;
        reverse(s.begin(),s.end());
        string text2 = s;
        vector<int>temp = prev;
        for(int idx1=1;idx1<n+1;idx1++){
            for(int idx2=1;idx2<n+1;idx2++){
                 if(text1[idx1-1] == text2[idx2-1])temp[idx2] = 1+prev[idx2-1];
                 else temp[idx2] = max(prev[idx2],temp[idx2-1]);
                 
            }
            prev = temp;
        }
        int longest_existing_pal_sequence =  prev[n];
        int min_insertion = n-longest_existing_pal_sequence;
        return min_insertion;
    
    }
};
```