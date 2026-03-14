# TCS_NQT_2026_Coding_Questions_Answers

### 1. cryptic_number

Code:
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
Code:
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

### 3. Prime Factor
Code:
```cpp
#include<bits/stdc++.h>
using namespace std;

int main(){
    int n;
    cin>>n;
    int temp=n;
    vector<int>ans;
    int i=3;
    while(n>1){
        if(n%2==0){
            ans.push_back(2);
            n/=2;
        }
        else{
            if(n%i==0 && i*i<=temp){
                ans.push_back(i);
                n/=i;
            }else if(n%i!=0 and i*i<=temp){
                i+=2;
            }
        }
    }
    for(auto it: ans){
        cout<<it<<" ";
    }
}
```

### 4. Move zeros to end
Code:
```cpp
#include<bits/stdc++.h>
using namespace std;

int main(){
    int n;
    cin>>n;
    vector<int>arr(n);

    for(int i=0; i<n;i++){
        cin>>arr[i];
    }

    int index=0;

    for(int i=0;i<n;i++){
        if(arr[i]!=0){
            arr[index]=arr[i];
            index++;
        }
    }

    for(int i=index;i<n;i++){
        arr[i]=0;
    }

    for(auto it: arr){
        cout<<it<<" ";
    }
    
}
```
### 5. good_bad_number
Code:
```cpp
#include<bits/stdc++.h>
using namespace std;

int main(){
    int n;

    cin>>n;
    while(n>0){
        int num;
        cin>>num;
        int original=num;
        int sum=0;
        while(num>0){
            int r=num%10;
            sum+=r;
            num/=10;
        }
        if(original%sum==0){
            cout<<"Good Number"<<endl;
        }else{
            cout<<"Bad Number"<<endl;
        }
        n--;
    }
}
```
### 6. Anagram

Given two non-empty strings s1 and s2, consisting only of lowercase English letters, determine whether they are anagrams of each other or not.
Two strings are considered anagrams if they contain the same characters with exactly the same frequencies, regardless of their order.

Examples:

Input: s1 = "geeks" s2 = "kseeg" \n
Output: true \n
Explanation: Both the string have same characters with same frequency. So, they are anagrams. \n
Input: s1 = "allergy", s2 = "allergyy" \n
Output: false 
Explanation: Although the characters are mostly the same, s2 contains an extra 'y' character. Since the frequency of characters differs, the strings are not anagrams. 
Input: s1 = "listen", s2 = "lists" 
Output: false 
Explanation: The characters in the two strings are not the same — some are missing or extra. So, they are not anagrams.
Constraints:
1 ≤ s1.size(), s2.size() ≤ 105
s1, s2 consists of lowercase English letters.

Code:
```cpp
#include <bits/stdc++.h>
using namespace std;

bool areAnagrams(string s1, string s2) {
    if (s1.length() != s2.length()) return false;

    int freq[26] = {0};

    for (char c : s1)
        freq[c - 'a']++;

    for (char c : s2)
        freq[c - 'a']--;

    for (int i = 0; i < 26; i++)
        if (freq[i] != 0)
            return false;

    return true;
}

int main() {
    string s1, s2;
    cin >> s1 >> s2;

    if (areAnagrams(s1, s2))
        cout << "true";
    else
        cout << "false";
}
```
