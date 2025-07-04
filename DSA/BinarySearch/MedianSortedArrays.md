# Median of Two Sorted Arrays

Start with the smallest array and mark the left and right bound. Suppose if the array is 
### vector<int> nums and it is small then we can continue with the right bound as its size
### Do binary search
**mid1=(left+right)>>1 and for mid2=(len1+len2+1)>>1 - mid1**
**Compare l1 with r2 and l2 with r1**
**If l1 is greater than r2 shift it leftwards: mid1=right-1;**
**And mid1=left+1**
