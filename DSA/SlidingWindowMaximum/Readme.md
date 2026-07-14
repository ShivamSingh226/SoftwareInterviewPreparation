# Problems

## Minimum Size Subarray Sum

```js
    // Maintain two pointers i=0 and j=0 and maintain a sum=0;
    for(int j=0;j<n;j++){
        sum+=arr[j];
        while(sum>=target){
            int minLen=min(minLen,j-i+i);
            sum-=arr[i++];
            
        }
    }
    return minLen==INT_MAX?0:minLen;

```

## Longest Substring without Repeating Characters

```js
//Maintain unordered_map<char,int> ump , int i and j and int maxLen
for(j=0;i<n;i++){
    if(!ump.count(s[j]) || ump[s[j]]<i){ // Check for both if not present or if it is outside the left bound of the array that we are checking
        ump[s[j]]=j;
        len=max(len,j-i+1);
    }else{
        i=ump[s[j]]+1;
        ump[s[j]]=j;

    }
}

```