
### Taro and Jiro will play the following game against each other.

Initially, they are given a sequence 𝑎=(𝑎1,𝑎2,…,𝑎𝑁). Until 𝑎a becomes empty, the two players perform the following operation alternately, starting from Taro:

- Remove the element at the beginning or the end of 𝑎. The player earns 𝑥 points, where 𝑥 is the removed element.

Let 𝑋 and 𝑌 be Taro's and Jiro's total score at the end of the game, respectively. Taro tries to maximize 𝑋−𝑌, while Jiro tries to minimize 𝑋−𝑌

Assuming that the two players play optimally, find the resulting value of 𝑋−𝑌
```
maximising x-y => x> y , minimising it => x< y
```

```python 
def solve(a):
'''
let dp[i][j] the maximum value of x-y for the sub array [i: j +1]
'''
    N = len(a)
    dp = [[0] * N for _ in range(N)]
    
    # Base case: when the subarray has only one element
    ''' if i == j : then the subarray is of size 1 , the max value is a[i]'''
    for i in range(N):
        dp[i][i] = a[i]
    
    # Fill the DP table
    
    #run bckwards sincd dp(i)(j) depends on (i+1)(j)
    for i in range(N-1, 0, -1):  
    # j is the ending point  of the subarray starting from i 
        for j in range(i+1,N):
            # if taro takes a[i], we are left with the array a[i+1:j] , since we computing x-y , then optimal y would be store in dp[i+1][j] , optimal answer in that case would be that take- optimal y 
            #if taro takes a[j] , we are left with the array a[i:j-1] , same logic 
            dp[i][j] = max(a[i] - dp[i+1][j], a[j] - dp[i][j-1])
    #return answr for all the list 
    return dp[0][N-1]




n= int(input())
lis=list(map(int, input().split()))
print(solve(lis))  

```