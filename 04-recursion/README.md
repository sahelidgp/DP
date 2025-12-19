# Print all subsequences of an array
```c++
#include <bits/stdc++.h>
using namespace std;

void print(vector<int>&list){
    if(list.size() == 0)
    {
        cout<<"{}"<<endl;
        return;
    }
    for(int i=0;i<list.size();i++)cout<<list[i];
    cout<<endl;
}
void subsequence(int ind,vector<int>list,vector<int>&arr){
    int n = arr.size();
    if(ind >= n){
        print(list);
        return;
    }
    list.push_back(arr[ind]);
    subsequence(ind+1,list,arr);
    list.pop_back();
    subsequence(ind+1,list,arr);
}
int main()
{
    vector<int>arr = {3,1,2};
    
    subsequence(0,{},arr);
    return 0;
}
```

# Print all subsequences with sum k

```c++
#include <bits/stdc++.h>
using namespace std;

void print(vector<int>&list){
    if(list.size() == 0)
    {
        cout<<"{}"<<endl;
        return;
    }
    for(int i=0;i<list.size();i++)cout<<list[i]<<" ";
    cout<<endl;
}
void subsequence(int ind,vector<int>&list,vector<int>&arr,int sum,int k){
    int n = arr.size();
    if(ind >= n){
        if(sum == k) print(list);
        return;
    }
    list.push_back(arr[ind]);
    sum += arr[ind],
    subsequence(ind+1,list,arr,sum,k);
    sum -= arr[ind],
    list.pop_back();
    subsequence(ind+1,list,arr,sum,k);
}
int main()
{
    vector<int>arr = {1,2,1};
    int k = 2;
    vector<int>list;
    subsequence(0,list,arr,0,k);
    return 0;
}
```