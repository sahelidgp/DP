# [Problem Link](https://leetcode.com/problems/delete-operation-for-two-strings/description/)

# Code❤️
```c++
class Solution {
public:
    int minDistance(string word1, string word2) {
        int len1 = word1.size();
        int len2 = word2.size();
        vector<int>prev(len2+1,0);
        vector<int>temp = prev;
        for(int idx1=1;idx1<len1+1;idx1++){
            for(int idx2=1;idx2<len2+1;idx2++){
                 if(word1[idx1-1] == word2[idx2-1])temp[idx2] = 1+prev[idx2-1];
                 else temp[idx2] = max(prev[idx2],temp[idx2-1]);
                 
            }
            prev = temp;
        }
        int lcs_len = prev[len2];

        int min_removal = len1+len2-2*lcs_len;
        return min_removal;
    }
};
```