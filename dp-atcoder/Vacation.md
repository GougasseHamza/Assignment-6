

### Problem Overview:

The code is solving a dynamic programming problem where, for each of the `n` days, there are 3 activities. The goal is to maximize the total value accumulated over the days, with the constraint that you can't perform the same activity on two consecutive days.
## my attempt : 
```python 
n= int(input()) lis=[[]] dp=[0]*(n+1) for i in range(n): t=list(map(int,input().split())) lis.append(t) dp[0]= max(lis[1]) banned = " " for i in range(1, n+1): 
for j in range(len(lis[i])) :
if j != banned and dp[i-1]+ lis[i][j] > dp[i]:
dp[i]= dp[i-1]+lis[i][j]
banned=j 
print(dp, banned )


```

### why is this wrong : 
#### incorrect dp logic , because i assume that dp[i-1] hold the answer for any day, while if so then the dp table should be two dimensional, and banned logic doesnt work at all 
### Explanation:

- **`dp` array**: This array keeps track of the maximum value that can be achieved up to the previous day (or the current day when updated) for each activity.
    
- **`new_dp` array**: This is a temporary array used to store the updated maximum values for the current day before they overwrite the previous day's values in the `dp` array.
    
### Why Use `new_dp`?

- **Avoid Overwriting**: If you directly update the `dp` array while iterating through the activities, you might overwrite a value that you still need to use to compute another `dp` value. For example, if you update `dp[0]` before calculating `dp[1]`, then when you calculate `dp[1]`, you'll be using an already updated value from `dp[0]`, which isn't what you want.
    
- **Correctness**: By using `new_dp`, you ensure that all calculations for the current day are based on the previous day's results (i.e., the original `dp` values) and not on partially updated values.






```python 
n = int(input())
lis = []
for _ in range(n):
    t = list(map(int, input().split()))
    lis.append(t)

dp  =[lis[0][0], lis[0][1], lis[0][2]]
for i in range(1, n):
    new_dp = [0] * 3
    for j in range(3):
        new_dp[j] = max(dp[(j+1) % 3] + lis[i][j], dp[(j+2) % 3] + lis[i][j])
    dp = new_dp

result = max(dp)
print(result )
--------------------
n = int(input())
lis = []
dp = [[0] * 3 for _ in range(n + 1)]

# Read input values
for _ in range(n):
    t = list(map(int, input().split()))
    lis.append(t)

# Initialization
dp[0][0] = lis[0][0]
dp[0][1] = lis[0][1]
dp[0][2] = lis[0][2]

# Fill the dp table
for i in range(1, n):
    dp[i][0] = max(dp[i-1][1], dp[i-1][2]) + lis[i][0]
    dp[i][1] = max(dp[i-1][0], dp[i-1][2]) + lis[i][1]
    dp[i][2] = max(dp[i-1][0], dp[i-1][1]) + lis[i][2]

# The result is the maximum value on the last day
result = max(dp[n-1][0], dp[n-1][1], dp[n-1][2])
print(result)

```


# DP with second loop over all the choices ( can be a 2d dp ) 
