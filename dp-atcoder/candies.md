
### There are 𝑁 children, numbered 1,2,…,𝑁.

They have decided to share 𝐾 candies among themselves. Here, for each 𝑖 (1≤𝑖≤𝑁), Child 𝑖 must receive between 0 and 𝑎𝑖 candies (inclusive). Also, no candies should be left over.

Find the number of ways for them to share candies, modulo 1e9+7. Here, two ways are said to be different when there exists a child who receives a different number of candies.


### my idea: 
#### let dp(i)(j) the nuber of ways to share j candies among i childs ( subarray [0:i+1] ) then dp(i)(j) will be the sum of the previous step (dp(i-1)(k)) for all k between 0 and a(i) , but if child i receive x amount of candies ( 0<=x<=a(i))  , then child (i-1) must have received j-x amount of candies, we then define j' = j-x which gives x = j'-j 
#### the sum becomes : 
![[Pasted image 20240814131436.png]]

#### but this is too slow it would add another for loop over k to calculate dp(i)(j) and then time complexity of ( nk^2)

## usage of prefix sum 
#### define pr[j] = sum of all dp(i-1)(k) from 0 to j 
#### we know then that somme of dp(i-1)(k) from a to b is pr(b)- pr(a-1)
#### given the boundary sum, dp(i)(j) will be pr(j)- pr(j-a(i)-1)
#### but the inequality has to make sure that j' >= j-ai , then if this is not valid, we have to add 0 
```python
MOD = 10**9 + 7

def count_ways_to_distribute_candies(N, K, a):
    dp = [[0] * (K + 1) for _ in range(N + 1)]
    dp[0][0] = 1  # Base case: 1 way to distribute 0 candies to 0 children

    for i in range(1, N + 1):
        max_candies = a[i - 1]
        prefix_sum = [0] * (K + 1)
        prefix_sum[0] = dp[i - 1][0]
        #calculatig prefix sum 
        for j in range(1, K + 1):
            prefix_sum[j] = (prefix_sum[j - 1] + dp[i - 1][j]) % MOD
        #using dp formula
        for j in range(K + 1):
            lower_bound = max(0, j - max_candies - 1)
            #if lower bound isnt valid, then we cant sum that state , we add simple 0 
            dp[i][j] = (prefix_sum[j] - (prefix_sum[lower_bound] if lower_bound >= 0 else 0) + MOD) % MOD

    return dp[N][K]

# Input reading
N, K = map(int, input().split())
a = list(map(int, input().split()))

print(count_ways_to_distribute_candies(N, K, a))


```








