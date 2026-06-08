# [Problem Link](https://leetcode.com/problems/partition-equal-subset-sum/description/)

# code(Sapce optimized)
```c++
class Solution {
public:
    bool canPartition(vector<int>& nums) {
        int n = nums.size();
        int Totsum = accumulate(nums.begin(),nums.end(),0);
        if(Totsum % 2)return false;
        int sum = Totsum/2;
        vector<bool>prev(sum+1,false);
        prev[0] = true;
        
        if(nums[0] <= sum)
        prev[nums[0]] = true;
        
        vector<bool>temp = prev;
        for(int ind = 1;ind<n;ind++){
                for(int target = 1;target<=sum;target++){
                bool notTake = prev[target];
                
                bool take = false;
                if(nums[ind] <= target){
                    take = prev[target-nums[ind]];
                    
                }
                temp[target] = take | notTake;
            }
            prev = temp;
        }
            
            
        return prev[sum];
    }
};
```