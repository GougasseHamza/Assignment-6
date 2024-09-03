given a grid (n, m) filled with  unreachable cells , find all the ways possible to the end 

#### very straightforward, base cases are first row and columnn, and for each position (i,j) dp(i)(j) holds the answer for that speicific position , if the cell is okay, we have two ways to reach that cell , hence dp(i)(j) is the sum of dp(i-1)(j) and dp(i)(j-1)



```python 
n, m = map(int, input().split())
lis = []

for _ in range(n):
    s = input()
    lis.append(list(s))  # Simplified to directly append the list of characters

dp = [[0 for _ in range(m)] for _ in range(n)]

# Base case: start point
dp[0][0] = 1 if lis[0][0] != '#' else 0

# Fill the first row
for i in range(1, m):
    if lis[0][i] == '#':
        dp[0][i] = 0
    else:
        dp[0][i] = dp[0][i-1]  # Only possible to come from the left

# Fill the first column
for i in range(1, n):
    if lis[i][0] == '#':
        dp[i][0] = 0
    else:
        dp[i][0] = dp[i-1][0]  # Only possible to come from above

# Fill the rest of the dp table
for i in range(1, n):
    for j in range(1, m):
        if lis[i][j] == '#':
            dp[i][j] = 0
        else:
            dp[i][j] = (dp[i-1][j] + dp[i][j-1]) % (10**9 + 7)

# Result
print(dp[n-1][m-1])


```







