### 1. Input:

- N is the number of coins, and it is a positive odd number.
- p is a list of length N, where each element p[i] represents the probability that the i-th coin lands heads.

### 2. DP Table Initialization:

- `dp[i][j]` will represent the probability of getting exactly jjj heads after tossing the first iii coins.
- The DP table is initialized with zeros: `dp = [[0] * (N + 1) for _ in range(N + 1)]`.
- `dp[0][0] = 1`: This is the base case, representing the probability of having 0 heads with 0 coins, which is 1.

### 3. Filling the DP Table:

- The outer loop iterates over each coin from 1 to NNN (inclusive).
- The inner loop iterates over the possible number of heads from 0 to iii (inclusive), where iii is the current coin index.
    - **When Coin i lands heads:** If j>0, the probability of having jjj heads after tossing iii coins includes the scenario where the first i−1coins had j−1 heads, and the current coin lands heads. This contribution is added to `dp[i][j]` as `dp[i - 1][j - 1] * p[i - 1]`.
    -     
    This is because, if the iii-th coin lands heads, then j−1j - 1j−1 heads must have been present in the previous i−1i - 1i−1 coins. The probability of the iii-th coin landing heads is p[i−1]p[i - 1]p[i−1].
    - **When Coin i lands tails:** The probability of having jjj heads also includes the scenario where the first i−1coins already had jjj heads, and the current coin lands tails. This contribution is added to `dp[i][j]` as `dp[i - 1][j] * (1 - p[i - 1])`.
    Here, if the iii-th coin lands tails, then jjj heads must have been present in the previous i−1i - 1i−1 coins. The probability of the iii-th coin landing tails is 1−p[i−1]1 - p[i - 1]1−p[i−1].
### 4. Calculating the Result:

- After filling the DP table, the result is calculated by summing up the probabilities of having more heads than tails.
- Since NNN is odd, the number of heads must be greater than N//2N // 2N//2 to have more heads than tails.
- The loop `for j in range((N // 2) + 1, N + 1)` sums up the probabilities in `dp[N][j]` for jjj values greater than N//2N // 2N//2.
```python 
N = int(input())  # N is a positive odd number
p = list(map(float, input().split()))  # list of probabilities

# Initialize DP table
dp = [[0] * (N + 1) for _ in range(N + 1)]
dp[0][0] = 1  # Base case: probability of 0 heads with 0 coins is 1

# Fill the DP table
for i in range(1, N + 1):
    for j in range(i + 1):
        if j > 0:
        #coin i lands heads , then we got j heads in the ith toss, which means we already had j-1 heads in i-1 toss 
            dp[i][j] += dp[i - 1][j - 1] * p[i - 1]  # Coin i lands heads
        #coin i lands tails , then we alr got j heads in i-1 toss 
        dp[i][j] += dp[i - 1][j] * (1 - p[i - 1])  # Coin i lands tails

# Calculate the probability of having more heads than tails
result = 0
for j in range((N // 2) + 1, N + 1):
    result += dp[N][j]

print(result)
```