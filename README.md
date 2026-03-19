# TCS_NQT_2026_Coding_Questions_Answers And IBM

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

Input: s1 = "geeks" s2 = "kseeg" 

Output: true 

Explanation: Both the string have same characters with same frequency. So, they are anagrams. 

Input: s1 = "allergy", s2 = "allergyy" 

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
## IBM Coding QNA:

### 7. Count Subarrays having Sum K

Code:
```cpp
#include <iostream>
#include <vector>
#include <unordered_map>
using namespace std;

int cntSubarrays(vector<int> &arr, int k) {
  
    // unordered_map to store prefix sums frequencies
    unordered_map<int, int> prefixSums;
  
    int res = 0;
    int currSum = 0;

    for (int i = 0; i < arr.size(); i++) {
        
        // Add current element to sum so far.
        currSum += arr[i];

        // If currSum is equal to desired sum, then a new
        // subarray is found. So increase count of subarrays.
        if (currSum == k)
            res++;

        // Check if the difference exists in the prefixSums map.
        if (prefixSums.find(currSum - k) != prefixSums.end())
            res += prefixSums[currSum - k];

        // Add currSum to the set of prefix sums.
        prefixSums[currSum]++;
    }

    return res;
}

int main() {
    vector<int> arr = {10, 2, -2, -20, 10};
    int k = -10;
    cout << cntSubarrays(arr, k);
    return 0;
}
```

### 8. Subarray with Given Sum - Handles Negative Numbers

Code:
```cpp
// C++ program to print subarray with sum as given sum
#include <bits/stdc++.h>
using namespace std;

// Function to print subarray with sum as given sum
void subArraySum(int arr[], int n, int sum)
{
    // create an empty map
    unordered_map<int, int> map;

    // Maintains sum of elements so far
    int curr_sum = 0;

    for (int i = 0; i < n; i++) {
        // add current element to curr_sum
        curr_sum = curr_sum + arr[i];

        // if curr_sum is equal to target sum
        // we found a subarray starting from index 0
        // and ending at index i
        if (curr_sum == sum) {
            cout << "Sum found between indexes " << 0
                 << " to " << i << endl;
            return;
        }

        // If curr_sum - sum already exists in map
        // we have found a subarray with target sum
        if (map.find(curr_sum - sum) != map.end()) {
            cout << "Sum found between indexes "
                 << map[curr_sum - sum] + 1 << " to " << i
                 << endl;
            return;
        }

        map[curr_sum] = i;
    }

    // If we reach here, then no subarray exists
    cout << "No subarray with given sum exists";
}

// Driver code
int main()
{
    int arr[] = { 2, 12, -2, -20, 10 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int sum = -10;

    // Function call
    subArraySum(arr, n, sum);

    return 0;
}
```

### 9. Sort 0s, 1s and 2s
Given an array arr[] containing only 0s, 1s, and 2s. Sort the array in ascending order.
Note: You need to solve this problem without utilizing the built-in sort function.

Examples:

Input: arr[] = [0, 1, 2, 0, 1, 2]

Output: [0, 0, 1, 1, 2, 2]

Explanation: 0s, 1s and 2s are segregated into ascending order.

Input: arr[] = [0, 1, 1, 0, 1, 2, 1, 2, 0, 0, 0, 1]

Output: [0, 0, 0, 0, 0, 1, 1, 1, 1, 1, 2, 2]

Explanation: 0s, 1s and 2s are segregated into ascending order.

Code:

```cpp
#include <bits/stdc++.h>
#include <algorithm>
using namespace std;

class Solution {
  public:
    void sort012(vector<int>& arr) {
        int zero=0;
        int one=0;
        int two=arr.size()-1;
        
        while(one<=two){
            if(arr[one]==0){
                swap(arr[zero++], arr[one++]);
            }
            else if(arr[one]==1){
                one++;
            }
            else{
                swap(arr[one], arr[two--]);
            }
        }
    }
};
```
