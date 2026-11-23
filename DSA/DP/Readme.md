# Dynammic Programming

## Best time to buy and sell stocks III

```js
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int n=prices.size();
        int dp[3][n];
        memset(dp,0,sizeof(dp));
        for(int i=1;i<=2;i++){
            int net_cash=0-prices[0];
            for(int j=1;j<n;j++){
                
                dp[i][j]=max(dp[i][j-1],prices[j]+net_cash); // Selling the stock ith transaction
                net_cash=max(net_cash,dp[i-1][j-1]-prices[j]); // Buying the stock i-1 transaction, still the transaction is not complete, j-1 choosing because buying the stock requires you to sell the stock before
            }
        }
        return dp[2][n-1];
    }
};
```

### Important Note:

1. `dp[i][j]=max(dp[i][j-1],prices[j]+net_cash);`: Selling the stock ith transaction is complete

2. `net_cash=max(net_cash,dp[i-1][j-1]-prices[j]);` : Buying the stock->i-1 transaction, still the transaction is not complete, j-1 choosing because buying the stock requires you to sell the stock before


## Edit Distance

### Subproblem of LCS


1. While tabulating, we calculate from `n` at **String1** and `m` at **String2**
2. So, if a letter is matched:
`When s1[i]==s2[j]`, then we should check for remaining string, except ` i and j`.
3. We decrease the iterator from ` i -> i-1`and ` j ->j-1`.
4. Now, we will look in range of `dp(i-1,j-1)`
5. So, we need a very small base case here like we do in LCS
```js
 vector<vector<int>>dp(n+1,vector<int>(m+1,INT_MAX-1));
        dp[0][0]=0;
        for(int i=1;i<=n;i++){
            dp[i][0]=i;
        }
        for(int j=1;j<=m;j++){
            dp[0][j]=j;
        }
```

And then afterwards:
```js
for(int i=1;to i==n){
    for(int j=1; to j==m){
        if(s1[i-1]!=s2[j-1]){
            dp[i][j]=min(dp[i-1][j-1],min(dp[i-1][j],dp[i][j-1]))+1;
            // dp[i-1][j-1] -> If we replace the character
            // dp[i][j-1] -> If we add a new character to String s1 which is equal to s2[j-1], so we do dp[i][j-1]
            // dp[i-1][j] -> If we delete the character so, i becomes 0->i-1
        }else{
            dp[i][j]=dp[i-1][j-1]; // Since the characters are same we don't need to do anything and we move one step back on each string; 0->i becomes 0->i-1 and 0->j becomes 0 to j-1
        }
    }
}
```