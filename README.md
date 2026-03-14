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
cpp```
