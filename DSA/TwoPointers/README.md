# Questions 

## 3 Sum
```js
// Sort the array first so that we can operate nums[i]+nums[j]+nums[k]==0

for(int i=0;i<n;i++){
    if(i>0 && nums[i]==nums[i-1])continue; // to check for iterating through i if there was ever a same value which we have found as there will be same value throughtout
    int low=i+1;
    int high=n-1;
    int target=0-nums[i];
    while(low<high){
        if(nums[low]+nums[high]>target){
            high--;
        }else if(nums[low]+nums[high]<target){
            low++;
        }else{
            vector<int> temp={nums[i],nums[low],nums[high]};
            ans.push_back(temp);
            while(low<high && nums[low]==temp[1]){
                low++;
            }
            while(low<high && nums[high]==temp[2]){
                high--;
            }
        }
    }
    
}
```

## Container with Most Water

```js
// Initialize both low and high variable
int low=0;
int high=n-1;
while(low<high){
    if(height[low]<height[high]){
        val=max(val,height[low]*(high-low));
        low++;
    }else{
        val=max(val,heigh[high]*(high-low));
        high--;
    }
}
```