There is a set 𝐴={𝑎1,𝑎2,…,𝑎𝑁}consisting of 𝑁 positive integers. Taro and Jiro will play the following game against each other.

Initially, we have a pile consisting of 𝐾 stones. The two players perform the following operation alternately, starting from Taro:

- Choose an element 𝑥 in 𝐴, and remove exactly 𝑥 stones from the pile.

A player loses when he becomes unable to play. Assuming that both players play optimally, determine the winner.
#### idea : backtrack + memoisation over k , k describes the state of a game if we remove a certain (x1,x2..xn ) stones or (y1,y2.ym) stones we might find the same k , then there is repeated work 
# solution :
```python 

```import sys

# Increase the recursion limit
sys.setrecursionlimit(10**6)  # Adjust the limit as needed

def solve(k, choices):
    mini = min(choices)
    memo = {}

    def backtrack(flag, k):
    #base cases : 
        if k in memo:
            return memo[k]
        if k < mini:
            return flag == 1  # First player wins if it's their turn and no move is 
        if flag == 1:  # First player's turn
            for x in choices:
            #backtrack( flag)-> true if flag player can win 
            # if the choice is valid and the seonc player looses , then that move forces the second player to loose, we return true 
                if k - x >= 0 and not backtrack(-flag, k - x):
                    memo[k] = True  # First player can force a win
                    return True
            memo[k] = False  # First player cannot force a win
        else:  # Second player's turn
            for x in choices:
                if k - x >= 0 and not backtrack(flag, k - x):
                    memo[k] = True  # Second player can force a win
                    return True
            memo[k] = False  # Second player cannot force a win
        
        return memo[k]

    return "First" if backtrack(1, k) else "Second"

# Example usage
n, k = map(int, input().split())  # Read the number of moves n and the total stones k
choices = list(map(int, input().split()))  # Read the possible moves
print(solve(k, choices))  # Solve the game and print the result
