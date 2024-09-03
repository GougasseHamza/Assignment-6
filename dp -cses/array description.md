# You know that an array has nnn integers between 1 and m, and the absolute difference between two adjacent values is at most 1.

# Given a description of the array where some values may be unknown, your task is to count the number of arrays that match the description.

# idea : 
```
let dp[i][v] the number of valid arrays  of  length i , using the value v 
if lis(i) is 0 then v can take any number from 1 to m , and for each v , we can only put v , v-1 or v+1 to be a good array, so the total number is  dp(i-1) (v )+ dp(i-1)(v-1)+dp(i-1)(v+1) if v -1 and v+1 are obv is the range(1,m)
if lis(i) is not 0 , we can only take lis(i-1) or lis(i+1) in the next step.
```
```python
n, m = map(int, input().split())
lis = list(map(int, input().split()))

# Initialize DP table
dp = [[0] * (m + 1) for _ in range(n)]

# Base case: Handle the first element
if lis[0] == 0:
    for v in range(1, m + 1):
        dp[0][v] = 1
else:
    dp[0][lis[0]] = 1

# Fill the DP table
for i in range(1, n):
    if lis[i] == 0:
        for v in range(1, m + 1): 
            # Start with the value from the previous row
            dp[i][v] = dp[i - 1][v]
            # Add values from adjacent positions
            for delta in (-1, 1):
                if 1 <= v + delta <= m:
                    dp[i][v] += dp[i - 1][v + delta]
    else:
        v = lis[i]
        dp[i][v] = dp[i - 1][v]
        for delta in (-1, 1):
            if 1 <= v + delta <= m:
                dp[i][v] += dp[i - 1][v + delta]

# Sum up all valid arrays ending at the last position
result = sum(dp[n - 1][v] for v in range(1, m + 1))

print(result)

```