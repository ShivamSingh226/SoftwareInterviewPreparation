# Questions

## Insert Interval

### intervals = [[1,2],[3,5],[6,7],[8,10],[12,16]], newInterval = [4,8]

```js
// So, we need to insert and merge this newInterval
xStart=newInterval[0];
xEnd=newInterval[1];
// The first case is when we are done merging interval that is:
for(int i=0->n){
    if(intervals[i][0]>xEnd){
        ans.push_back({xStart,xEnd});
        // Now, we update new Boundary to so that we can merge another interval if possible
        xStart=intervals[i][0];
        xEnd=intervals[i][1];
    }else if(intervals[1][1]>=xStart){
        xStart=min(xStart,intervals[i][0]);
        xEnd=max(xEnd,intervals[i][1]);
        // Here, we update the boundaries so that we can merge as after first case, we know that this interval would surely merge
    }else{
        ans.push_back(intervals[i]); // Any intervals who are overall less than the given interval; who come before that interval
    }
}

```


## Minimum number of Arrows to burst balloons

**Sort The array by second element**
`sort(a.begin(),a.end(),[&](vector<int> &x,vector<int> &y){
    return x[1]< y[1];
})`
```js
// Very similar question for merging interval,
// 1. To minimize the number of arrows to burst ballon we need to ensure that they intersect

// 2. The start of the boundary of the interval should be less than the previous interval's end

// 3. When it is not, we increase cnt++; and we update the end interval;

// 4. Also, make sure 
int end=interval[0][1];
int cnt=1;
for(int i=1->n){

    if(interval[i][0]>end){
        cnt++;
        end=interval[i][1];
    }
}
```