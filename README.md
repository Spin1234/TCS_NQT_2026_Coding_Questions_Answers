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
### 10. GCD of two numbers
Code:
```cpp
class Solution {
  public:
    int gcd(int a, int b) {
        if(b==0) return a;
        return gcd(b, a%b);
    }
};
```
### 11. LCM of two numbers
Code:
```cpp
class Solution {
  public:
    int gcd(int a, int b){
        if(b==0) return a;
        return gcd(b,a%b);
    }
    int lcm(int a, int b) {
        int hcf=gcd(a,b);
        int lcm = a*b/hcf;
        return lcm;
        
    }
};
```
### 12. Two Sum
Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

You can return the answer in any order.

 

Example 1:

Input: nums = [2,7,11,15], target = 9

Output: [0,1]

Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].

Example 2:

Input: nums = [3,2,4], target = 6

Output: [1,2]

Example 3:

Input: nums = [3,3], target = 6

Output: [0,1]

Code:
```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {

        vector<int>ans;

        for(int i=0; i<nums.size()-1; i++){
            for(int j=i+1; j<nums.size(); j++){
                if(nums[i]+nums[j]==target){
                    ans.push_back(i);
                    ans.push_back(j);
                }
            }
        }

        return ans;
    }
};
```
### 13. Maximum Subarray
Given an integer array nums, find the subarray with the largest sum, and return its sum.

 

Example 1:

Input: nums = [-2,1,-3,4,-1,2,1,-5,4]

Output: 6

Explanation: The subarray [4,-1,2,1] has the largest sum 6.

Example 2:

Input: nums = [1]

Output: 1

Explanation: The subarray [1] has the largest sum 1.

Example 3:

Input: nums = [5,4,-1,7,8]

Output: 23

Explanation: The subarray [5,4,-1,7,8] has the largest sum 23.

Code:
```cpp
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int maxsum=INT_MIN;
        int currsum=0;
        for(int i=0; i<nums.size(); i++){
            currsum+=nums[i];
            if(maxsum<currsum){
                maxsum=currsum;
            }
            if(currsum<0){
                currsum=0;
            }
        }
        return maxsum;
    }
};
```
### 14. Longest Subarray with Sum K
Given an array arr[] containing integers and an integer k, your task is to find the length of the longest subarray where the sum of its elements is equal to the given value k. If there is no subarray with sum equal to k, return 0.

Code:
```cpp
class Solution {
public:
    int longestSubarray(vector<int>& arr, int k) {
        
        unordered_map<int, int> mp; // prefixSum -> index
        
        int sum = 0;
        int maxLen = 0;

        for (int i = 0; i < arr.size(); i++) {
            sum += arr[i];

            // Case 1: from index 0 to i
            if (sum == k) {
                maxLen = i + 1;
            }

            // Case 2: subarray exists
            if (mp.find(sum - k) != mp.end()) {
                int len = i - mp[sum - k];
                maxLen = max(maxLen, len);
            }

            // Store only first occurrence
            if (mp.find(sum) == mp.end()) {
                mp[sum] = i;
            }
        }

        return maxLen;
    }
};
```
### 15. Group Anagram Frequency Tracker

---

# Group Anagram Frequency Tracker

## Problem Description
You are given a vector of **N** strings and **Q** queries. Each query contains a string, and you need to determine how many anagrams of that query string exist in the original vector. 

Two strings are **anagrams** if they contain the same characters with the same frequencies, regardless of order. You must preprocess the vector efficiently to handle multiple queries quickly using hashmaps or collections.

Your task is to build a frequency map where strings that are anagrams of each other are grouped together, then answer each query by returning the count of strings in the vector that are anagrams of the query string.

## Function Description
Implement the function `countAnagramGroups`. The function should:
1. Preprocess the vector of strings by grouping anagrams together using a hashmap.
2. For each query string, return the count of its anagrams found in the original vector.

### Parameters
* **N**: An integer representing the number of strings in the vector.
* **Q**: An integer representing the number of queries.
* **strings**: A vector/list of N strings from the original vector.
* **queries**: A vector/list of Q strings representing the query strings.

### Returns
* A vector of **Q** integers where each integer represents the count of anagrams for the corresponding query string.

---

## Input Format
1. The first line contains a single integer **N**.
2. The second line contains **N** space-separated strings.
3. The third line contains a single integer **Q**.
4. The fourth line contains **Q** space-separated strings representing the queries.

## Output Format
Print a single line containing **Q** space-separated integers representing the count of anagrams for each corresponding query.

---

## Constraints
* $1 \le N \le 10^5$
* $1 \le Q \le 10^5$
* $1 \le \text{length of each string} \le 100$
* All strings contain only lowercase English letters ('a' to 'z').
* Total characters across all strings $\le 10^6$

---

## Example
**Sample Input 1**
```text
6
listen silent enlist google googlg inlets
3
silent google test
```

**Sample Output 1**
```text
4 2 0
```

**Explanation**
* **Query 1 ("silent"):** The anagrams in the vector are "listen", "silent", "enlist", and "inlets". (All contain letters: e, i, l, n, s, t). **Count = 4**.
* **Query 2 ("google"):** The anagrams in the vector are "google" and "googlg". (Both contain letters: g, g, l, o, o, e). **Count = 2**.
* **Query 3 ("test"):** No anagrams of "test" exist in the vector. **Count = 0**.

Code:
```cpp
#include <bits/stdc++.h>
using namespace std;

vector<int> groupAnagrams(int N, vector<string>& strings, int Q, vector<string>& queries) {
    unordered_map<string, int> freq;

    // Step 1: Build frequency map
    for (string s : strings) {
        string key = s;
        sort(key.begin(), key.end());
        freq[key]++;
    }

    // Step 2: Answer queries
    vector<int> result;
    for (string q : queries) {
        string key = q;
        sort(key.begin(), key.end());

        if (freq.find(key) != freq.end())
            result.push_back(freq[key]);
        else
            result.push_back(0);
    }

    return result;
}

int main() {
    int N;
    cin >> N;

    vector<string> strings(N);
    for (int i = 0; i < N; i++) {
        cin >> strings[i];
    }

    int Q;
    cin >> Q;

    vector<string> queries(Q);
    for (int i = 0; i < Q; i++) {
        cin >> queries[i];
    }

    vector<int> ans = groupAnagrams(N, strings, Q, queries);

    for (int x : ans) {
        cout << x << " ";
    }

    return 0;
}
```

Complete Code:
```cpp
#include<bits/stdc++.h>
using namespace std;

int main(){
    vector<string>strings;
    int n;
    cin>>n;
    for(int i=0; i<n; i++){
        string data;
        cin>>data;
        strings.push_back(data);
    }

    vector<string>queries;
    int q;
    cin>>q;
    for(int i=0; i<q; i++){
        string data;
        cin>>data;
        queries.push_back(data);
    }

    unordered_map<string,int>freq;

    for(string s: strings){
        string key = s;
        sort(key.begin(),key.end());
        freq[key]++;
    }

    vector<int>ans;
    for(string q:queries){
        string key = q;
        sort(key.begin(),key.end());
        if(freq.find(key)!=freq.end()){
            ans.push_back(freq[key]);
        }else{
            ans.push_back(0);
        }
    }

    for(auto it:ans){
        cout<<it<<" ";
    }

}
```

---

