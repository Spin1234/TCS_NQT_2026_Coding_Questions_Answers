# TCS_NQT_2026_Coding_Questions_Answers

### 1. cryptic_number

### Code:
```cpp
#include<bits/stdc++.h>
using namespace std;

bool hasRepetedDigit(int num){
    int n = to_string(num).length();

    unordered_map<int, int>m;

    while (num>0)
    {
        int r = num%10;
        m[r]++;
        num/=10;
    }
    for (auto it: m)
    {
        if(it.second>1){
            return true;
        }
    }
    return false;
}

int main(){
    int c=0;
    for (int i = 5; i <=45; i++)
    {
        string str=to_string(i);
        string rev=str;
        reverse(rev.begin(), rev.end());
        if(i%7==0 && i%5!=0){
            if(!hasRepetedDigit(i) && rev!=str){
                c++;
                cout<<i<<" ";
            }
        }
    }
    if(c==0){
        cout<<"Not found!"<<endl;
    }
}
```
### 2. Rotate Array By D:
code:
```cpp
#include<bits/stdc++.h>
using namespace std;

// Naive approach, time com - O(n*d)
void rotateArrNaive(vector<int>&arr, int d){
    for (int i = 0; i < d; i++)
    {
        int first=arr[0];
        for (int j = 0; j < arr.size()-1; j++)
        {
            arr[j]=arr[j+1];
        }
        arr[arr.size()-1]=first;
        
    }
    
}

//Better Approach, time com - O(n)
void rotateArrTempArr(vector<int>&arr, int d){

    int n = arr.size();
    d %= n;
    vector<int>temp(n);

    for (int i = 0; i < n-d; i++)
    {
        temp[i]=arr[d+i];
    }
    for (int i = 0; i < d; i++)
    {
        temp[n-d+i]=arr[i];
    }
    for (int i = 0; i < n; i++)
    {
        arr[i]=temp[i];
    }
}

void rotateArrrReverse(vector<int>&arr, int d){
    d=d%arr.size();
    reverse(arr.begin(), arr.begin()+d);
    reverse(arr.begin()+d, arr.end());
    reverse(arr.begin(), arr.end());
}

int main(){

    int n=3;
    int d = 4;

    vector<int> arr={1,2,3};

    //rotateArrTempArr(arr, d);
    //rotateArrNaive(arr,d);
    rotateArrrReverse(arr,d);


    for (int i = 0; i < n; i++)
    {
        cout<< arr[i]<< " ";
    }
    
}
```
