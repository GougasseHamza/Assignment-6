#### There is a tree with 𝑁 vertices, numbered 1,2,…,𝑁For each 𝑖i (1≤𝑖≤𝑁−1) , the 𝑖-th edge connects Vertex 𝑥𝑖 and 𝑦𝑖​.

Taro has decided to paint each vertex in white or black. Here, it is not allowed to paint two adjacent vertices both in black.

Find the number of ways in which the vertices can be painted, modulo 10^9+7.

### idea obvious a dfs , but within each dfs call , we need to update a dp table given this notice
![[Pasted image 20240814135847.png]]

```python
MOD = 10**9 + 7

def dfs(v, parent):
    dp[v][0] = 1  # dp[v][0] represents the number of ways to paint subtree rooted at v with v white
    dp[v][1] = 1  # dp[v][1] represents the number of ways to paint subtree rooted at v with v black
    
    for u in adj[v]:
        if u == parent:
            continue
        dfs(u, v)
        # Number of ways to paint subtree rooted at v with v white
        dp[v][0] = (dp[v][0] * dp[u][1]) % MOD
        # Number of ways to paint subtree rooted at v with v black
        dp[v][1] = (dp[v][1] * (dp[u][0] + dp[u][1]) % MOD) % MOD

n = int(input())
adj = [[] for _ in range(n)]
dp = [[0] * 2 for _ in range(n)]

for _ in range(n - 1):
    a, b = map(int, input().split())
    a -= 1
    b -= 1
    adj[a].append(b)
    adj[b].append(a)

dfs(0, -1)
print((dp[0][0] + dp[0][1]) % MOD)

```