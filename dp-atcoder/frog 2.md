# Problem statement : 
There are **N** stones, numbered 1, 2, …, N. For each **i** (1 ≤ i ≤ N), the height of Stone **i** is **h_i**.

There is a frog who is initially on Stone 1. He will repeat the following action some number of times to reach Stone N:

If the frog is currently on Stone **i**, jump to one of the following: Stone **i+1, i+2, …, i+K**. Here, a cost of **|h_i − h_j|** is incurred, where **j** is the stone to land on.

Find the minimum possible total cost incurred before the frog reaches Stone N.

### same idea as frog 1 but then we loop over all possible k before i which is i-k 
```python 

n, k = map(int, input().split())

lis = list(map(int, input().split()))

dp = [float('inf')] * n
dp[0] = 0  

for i in range(1, n):
    for j in range(max(0, i - k), i):
        dp[i] = min(dp[i], dp[j] + abs(lis[i] - lis[j]))
        
print(dp[-1])
```
