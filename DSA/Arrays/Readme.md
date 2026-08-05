# 9th July 2026

## Remove Element

```js
// Maintain a variable
int index=0;
//Iterate through the for loop
for(;;;){
    if(nums[index]!=val){
        nums[index]=nums[i];
        index++;
    }
}
return index;
```
## Index of the first occurence of the String

```js
//For handling base case where size of needle is bigger than the haystack, return false;
for(;;;){
    st.substr(i,len_of_needle)return i;
}
return -1;
```

## Merge Sorted Arrays

```js
//
void merge(vector<int> &nums1, int m, vector<int> &nums2,int n){
    int i=m-1;
    int j=n-1;
    int k=m+n-1;
    //Iterate while loop
    while(i>=0 && j>=0){
        if(nums2[j]>nums1[i]){
            nums1[k]=nums2[j];
            k--;
            j--;
        }else{
            nums1[k]=nums1[i];
            k--;
            i--;
        }
    }
    while(i>=0){
        nums1[k]=nums1[i];
        k--;
        i--;
    }
    while(j>=0){
        nums1[k]=nums2[j];
        k--;
        j--;
    }
}
```

## 30th July 2026

## Removing Duplicates

```js

// Maintain a variable cnt=0;
// Iterate through for loop
for(num:nums){
    if(cnt<no_of_values_we_want || num>nums[cnt-no_of_values_we_want]){
        nums[cnt++]=num;
    }
}
return cnt;
```

## Majority Element [n/2] elements in an array

```js
int cnt=0;
int elem=0;
// Iterate through the array
for(num:nums){
    if(cnt==0){
        elem=num;
    }
    if(elem==num){
        cnt++;
        // Increase the counter if the element is same
    }else{
        cnt--;
        // Decrease the counter if the element is not same
    }
}
return elem;
// If a majority element is present it will be present at most times compared to other element even if we keep on substracting the cnt while iteration
```

## 5th August 2026

## Rotate Array
```js
/// The k would be mod by n
k=k%n
vector<int> temp;
for(int i=n-k;i<n;i++){
    temp.push_back(nums[i]);
}

for(int i=0;i<n-k;i++){
    temp.push_back(nums[i]);
}
nums=temp;

// Or
// 
reverse(nums.begin(),nums.begin()+(n-k));
reverse(nums.begin()+n-k,nums.end());
reverse(nums.begin(),nums.end());
```