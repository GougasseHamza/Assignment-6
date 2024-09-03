### There are 𝑁 flowers arranged in a row. For each 𝑖i (1≤𝑖≤𝑁), the height and the beauty of the 𝑖-th flower from the left is ℎ𝑖​ and 𝑎𝑖, respectively. Here, ℎ1,ℎ2,…,ℎ𝑁​ are all distinct.

Taro is pulling out some flowers so that the following condition is met:

- The heights of the remaining flowers are monotonically increasing from left to right.

Find the maximum possible sum of the beauties of the remaining flowers.

![[Pasted image 20240814141311.png]]

```c++
#include <iostream>
#include <vector>
#include <algorithm>
#include <climits>
using namespace std;

const int MAXN = 200005; // Adjust if needed
const long long NEG_INF = LLONG_MIN;

class SegmentTree {
public:
    SegmentTree(int size) : n(size) {
        data.assign(4 * size, 0);
    }

    void update(int idx, long long value, int l = 1, int r = MAXN, int pos = 1) {
        if (l == r) {
            data[pos] = max(data[pos], value);
        } else {
            int mid = (l + r) / 2;
            if (idx <= mid) {
                update(idx, value, l, mid, 2 * pos);
            } else {
                update(idx, value, mid + 1, r, 2 * pos + 1);
            }
            data[pos] = max(data[2 * pos], data[2 * pos + 1]);
        }
    }

    long long query(int ql, int qr, int l = 1, int r = MAXN, int pos = 1) {
        if (qr < l || ql > r) {
            return (long long ) 0;
        }
        if (ql <= l && r <= qr) {
            return data[pos];
        }
        int mid = (l + r) / 2;
        return max(query(ql, qr, l, mid, 2 * pos), query(ql, qr, mid + 1, r, 2 * pos + 1));
    }

private:
    int n;
    vector<long long> data;
};

int main() {
    int N;
    cin >> N;

    vector<int> heights(N + 1);
    vector<long long> beauties(N + 1);

    for (int i = 1; i <= N; ++i) {
        cin >> heights[i];
    }
    for (int i = 1; i <= N; ++i) {
        cin >> beauties[i];
    }

    // Use a segment tree with size `N` or `MAXN` based on maximum height in the input
    SegmentTree segTree(MAXN); // Adjust if necessary based on maximum height

    long long result = 0;

    for (int i = 1; i <= N; ++i) {
        // Query the maximum sum for flowers with heights less than the current height
        long long max_sum_before = segTree.query(1, heights[i] - 1);
        long long current_sum = max_sum_before + beauties[i];
         
        result = max(result, current_sum);

        // Update the segment tree with the current height and beauty sum
        segTree.update(heights[i], current_sum);

       

        
    }

    cout  << result << endl;
    return 0;
}

```