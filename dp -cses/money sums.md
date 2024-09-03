
You have nnn coins with certain values. Your task is to find all money sums you can create using these coins.

# Input

The first input line has an integer n: the number of coins.

The next line has n integers x1,x2,…,xn​: the values of the coins.

# Output

First print an integer k: the number of distinct money sums. After this, print all possible sums in increasing order.


# idea :
#### maintain a dp state that holds all possible answer for the array of length i, at each iteration, copy those elements to the dp(i+1) and add all possible sums using the element 
#### time complexity o(n*k )

#### official solution :
This is a case of the classical problem called 0-1 knapsack.

dp(i)(x)= true if it is possible to make x using the first i coins, false otherwise.

It is possible to make x with the first i coins, if either it was possible with the first i-1 coins, or we chose the i'th coin, and it was possible to make x — <value of i'th coin> using the first i-1 coins.

```c++ 

int main() {
  int n;
  cin >> n;
  int max_sum = n*1000;
  vector<int> x(n);
  for (int&v : x) cin >> v;
  vector<vector<bool>> dp(n+1,vector<bool>(max_sum+1,false));
  dp[0][0] = true;
  for (int i = 1; i <= n; i++) {
    for (int j = 0; j <= max_sum; j++) {
    //possible to make it with first i coins 
      dp[i][j] = dp[i-1][j];
      int left = j-x[i-1];
      // it has to be possible with j- ith coin 
      if (left >= 0 && dp[i-1][left]) {
	dp[i][j] = true;
	//else false 
      }
    }
  }

  vector<int> possible;
  for (int j = 1; j <= max_sum; j++) {
    if (dp[n][j]) {
      possible.push_back(j);
    }
  }
  cout << possible.size() << endl;
  for (int v : possible) {
    cout << v << ' ';
  }
  cout << endl;
}
```

