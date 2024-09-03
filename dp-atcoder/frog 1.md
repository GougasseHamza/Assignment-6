## Problem Statement

There are **N** stones, numbered **1, 2, …, N**. For each **i** (**1 ≤ i ≤ N**), the height of Stone **i** is **h_i**.

There is a frog who is initially on Stone **1**. He will repeat the following action some number of times to reach Stone **N**:

- If the frog is currently on Stone **i**, he can jump to Stone **i+1** or Stone **i+2**. Here, a cost of **|h_i - h_j|** is incurred, where **j** is the stone he lands on.

Find the minimum possible total cost incurred before the frog reaches Stone **N**.

### Idea : 
### let dp[i] the cost to reach i-th position, to reach that state, we can either jump from state i-1 or state i-2 , and respetively add the cost, so we  take the minimum . 

```python 
n = int(input())

# Input the list of heights
lis = list(map(int, input().split()))

# Initialize dp array
dp = [0] * n
dp[0] = 0  # No cost to stay on the first stone
dp[1] = abs(lis[1] - lis[0])

# Calculate the minimum cost for each stone
for i in range(2, n):
    dp[i] = min(dp[i-1] + abs(lis[i] - lis[i-1]), dp[i-2] + abs(lis[i] - lis[i-2]))

# Output the minimum cost to reach the last stone
print(dp[-1])
```




