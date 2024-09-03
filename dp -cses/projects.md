There are nnn projects you can attend. For each project, you know its starting and ending days and the amount of money you would get as reward. You can only attend one project during a day.

What is the maximum amount of money you can earn?

### classic problem we did in algo but this time weights are included 
### lets define dp(i ) the maxi reward for the subaraay endind at index(i+1) ( processing index i) , so if we sort the array with their ending time , for each index , we should find the last project doesnt conflict with project i , i was thinking maybe we should take the one with max reward... but no , if we take the last and instead increment that dp(i if ith element i taken) by dp of that index, that dp(index) already stores the best sum possible, so redandant work is avoided :) 

```c++
#include <bits/stdc++.h>

using namespace std;

struct Project {

int start, end, reward;

};

// Binary search to find the latest project that doesn't overlap with the current one

int findLastNonConflicting(vector<Project>& projects, int index) {

int low = 0, high = index - 1;

while (low <= high) {

int mid = low + (high - low) / 2;

if (projects[mid].end < projects[index].start) {

if (projects[mid + 1].end < projects[index].start) {

low = mid + 1;

} else {

return mid;

}

} else {

high = mid - 1;

}

}

return -1;

}

long long maxReward(vector<Project>& projects) {

int n = projects.size();

sort(projects.begin(), projects.end(), [](Project& a, Project& b) {

return a.end < b.end;

});

vector<long long > dp(n, 0);

dp[0] = projects[0].reward;

for (int i = 1; i < n; ++i) {

long long inclReward = projects[i].reward;

int l = findLastNonConflicting(projects, i);

if (l != -1) {

inclReward += dp[l];

}

dp[i] = max(dp[i - 1], inclReward);

}

return dp[n - 1];

}

int main() {

int n;

cin >> n;

vector<Project> projects(n);

for (int i = 0; i < n; ++i) {

cin >> projects[i].start >> projects[i].end >> projects[i].reward;

}

cout << maxReward(projects) << endl;

return 0;
```




