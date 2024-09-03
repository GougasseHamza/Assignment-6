
There are 𝑁 slimes lining up in a row. Initially, the 𝑖-th slime from the left has a size of 𝑎𝑖​.

Taro is trying to combine all the slimes into a larger slime. He will perform the following operation repeatedly until there is only one slime:

- Choose two adjacent slimes, and combine them into a new slime. The new slime has a size of 𝑥+𝑦, where 𝑥 and 𝑦 are the sizes of the slimes before combining them. Here, a cost of 𝑥+𝑦is incurred. The positional relationship of the slimes does not change while combining slimes.

Find the minimum possible total cost incurred

## idea : be greedy and always take the two minimums: not working 
### dp approach , divide the sub array into windows(i,j) , for every window, for every breaking point k between (i,j) calculate the cost of merging the slimes

```python
# Read input
n = int(input())
a = list(map(int, input().split()))
'''
let dp(i)(j) the min cost for subarray (i,j)
'''
# Prefix sum array for quick sum calculation
prefix_sum = [0] * (n + 1)
for i in range(n):
    prefix_sum[i + 1] = prefix_sum[i] + a[i]

# Initialize dp table
dp = [[float('inf')] * n for _ in range(n)]
dp(0)(0)= 0
'''
to merge (i,j) into one slime , we consider every breaking point k , the cost then will be the cost to split from i tok + to cost to split from k+1 to j , + the cost to merge the two splits, which is the sum over all the subarray (i,j )
'''
# Fill the DP table
for length in range(2, n + 1):  # subarray lengths
    for i in range(n - length + 1):
        j = i + length - 1
        dp[i][j] = float('inf')
        for k in range(i, j):
            cost = dp[i][k] + dp[k + 1][j] + (prefix_sum[j + 1] - prefix_sum[i])
            dp[i][j] = min(dp[i][j], cost)

# The answer is the cost to combine all slimes
print(dp[0][n - 1])

```