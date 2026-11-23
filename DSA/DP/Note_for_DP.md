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