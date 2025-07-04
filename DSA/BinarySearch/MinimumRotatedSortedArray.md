# Minimum in Rotated Sorted Array
**vector<int> nums ; Define left bound(l=0) and right(r=n-1).**
### If nums[l]<=nums[r] already we have got the answer otherwise we will obtain:
**ans=min(ans,nums[mid]) and then**
**if(nums[mid]>=nums[l]) l=mid+1**
**else r=mid-1**
