# [Problem Link](https://www.geeksforgeeks.org/problems/shortest-common-supersequence0322/1)

# Code❤️
```c++
class Solution {
  public:
    int minSuperSeq(string &s1, string &s2) {
        // code here
         int len1 = s1.size();
        int len2 =  s2.size();
        vector<int>prev(len2+1,0);
        vector<int>temp = prev;
        for(int idx1=1;idx1<len1+1;idx1++){
            for(int idx2=1;idx2<len2+1;idx2++){
                 if(s1[idx1-1] == s2[idx2-1])temp[idx2] = 1+prev[idx2-1];
                 else temp[idx2] = max(prev[idx2],temp[idx2-1]);
                 
            }
            prev = temp;
        }
        int lcs_len = prev[len2];

        int min_insertion = len1+len2-2*lcs_len;
        return min_insertion+lcs_len;
    }
};
```