# You are given an integer n. On each step, you may subtract one of the digits from the number.

# How many steps are required to make the number equal to 0?


## idea : backtracking over the digits of n with memo : 
```c++
#include <iostream>

#include <iostream>

#include <unordered_map>

#include <climits>

#include <string>

using namespace std;

// Memoization map

unordered_map<int, long long > memo;

// Recursive function to find minimum steps

long long minSteps(int n) {

// Check if the result is already computed

if (memo.find(n) != memo.end()) {

return memo[n];

}

// Base case: if n is 0, no steps are needed

if (n == 0) {

return (long long ) 0;

}

long long result = INT_MAX;

string numStr = to_string(n);

for (char digitChar : numStr) {

int digit = digitChar - '0';

if (digit != 0) { // Avoid subtracting 0 as it doesn't change the number

result = min(result, minSteps(n - digit) + 1);

}

}

memo[n] = result;

return result;

}

int main() {

int n;

cin >> n;

cout <<minSteps(n) << endl ;

return 0;

}
```



