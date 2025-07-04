# Finding the element in rotated search array
**Let's first fix the basic base condition in a Binary Search array**
### If nums[mid]<nums[r]
    **if nums[mid]<target && nums[r]>=target l=mid+1**
    else r=mid-1
### else
    if nums[mid]>target && nums[l]<=target r=mid-1**
    else l=mid+1

