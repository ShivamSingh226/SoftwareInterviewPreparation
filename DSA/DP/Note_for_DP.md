# Identification of Dynamic Programming

### How to identify?

1. Recursion (Where one subproblem is already getting solved somewhere in another branch)
2. Optimal Solution (Min,Max,Largest, Smallest)

| Top-Down | Bottom-Up DP |
| --- | --- |
| Starts at `n` recruses down to base case| Starts at base-case and then builds up |
| Recursion + Memoization | Loops and DP Table | 

### Standard DP Problems

1. 0-1 Knapsack
2. Unbounded Knapsack
3. Longest Common Subsequence
4. MCM

## Longest Common Subsequence

1. Base Condition(Think of smallest valid input or extreme where the code will end)-> Choice Based Recursion (Take it or not, A or B) -> Recursion call on next group


### Recursive + Memoization

```js

int dp(){
    if(i==0 || j==0){
        return 0;   // If anyone of the length becomes 0 then the Longest common Subsequence would only be an empty string
    }
    if(dp[i][j]!=-1){
        return dp[i][j];
    }
    if(s1[i-1]==s2[j-1]){
        return dp[i][j]=dp(i-1,j-1);
    }
    return dp[i][j]=max(dp(i-1,j),dp(i,j-1)); // Checking both of the strings where the given character matches and then returning the longest value
    
}
```

### Bottom-Up Tabulation

```js
dp[0][0]=0;
for(int i=0;i<=n;i++){
    dp[i][0]=0;
}
for(int j=0;j<=m;j++){
    dp[0][j]=0;
}
for(int i=1;i<=n;i++){
    for(int j=1;j<=n;j++){
        if(s1[i-1]!=s2[j-1]){
            dp[i][j]=max(dp[i][j-1],dp[i-1][j]);
        }else{
            dp[i][j]=dp[i-1][j-1]+1;
        }
    }
}
return dp[n][m];
```

## Knapsack Variation and Problems

**Note:** For unbounded Knapsack, ***weight parameter doesn't need to be subtracted*** in recursion or the DP Array.