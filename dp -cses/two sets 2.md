Your task is to count the number of ways numbers 1,2,…,n can be divided into two sets of equal sum.

For example, if n=7 ,  there are four solutions:

- {1,3,4,6} and {2,5,7}
- {1,2,5,6} and {3,4,7}
- {1,2,4,7} and {3,5,6}
- {1,6,7} and {2,3,4,5}
# little bit of math : 
#### let two sets a, b verfying the conditions , we know that the sum of a and b will be sum of 1..n which is n(n+1)/2 , so if this sum isnt odd, then there is no possible answer
#### secondly, since the sum of the two sets are equal , the sum of one set should be exactly n(n+1)/4 

#### the problem becomes a classic knapsawk 0-1 with weight being n(n+1)/4 

```c++
#include <iostream>

#include <vector>

using namespace std;

int main() {

int n;

cin >> n;

long long totalSum = n * (n + 1LL) / 2;

// Check if the total sum is divisible by 2

if (totalSum % 2 != 0) {

cout << 0 << endl;

return 0;

}

long long goal = totalSum / 2;

const int MOD = 1e9 + 7;

vector<int> dp(goal + 1, 0);

dp[0] = 1; // There's one way to make a sum of 0, by choosing nothing

for (int i = 1; i <= n; ++i) {

for (long long j = goal; j >= i; --j) {

dp[j] = (dp[j] + dp[j - i]) % MOD;

}

}

long long ans = dp[goal];




// Since every partition is counted twice, divide by 2 using modular inverse

long long result = (ans * ((MOD + 1) / 2)) % MOD;

cout << result << endl;

return 0;
}
```

