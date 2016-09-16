# 1068 : RMQ-ST算法
> http://hihocoder.com/problemset/problem/1068

## Solution 1:
```cpp
#include <iostream>
#include <algorithm>
using namespace std;

const int MAXN = 1000010;
int pre_calc[MAXN][21];

int main() {
	int N, Q;
	scanf("%d", &N);
	for (int j = 0; (1 << j) <= N; ++j) {
		for (int i = 1; i <= N; ++i) {
			if (j == 0)
				scanf("%d", &pre_calc[i][0]);
			else if ((i + (1 << j)) <= N)
				pre_calc[i][j] = min(pre_calc[i][j - 1], pre_calc[i + (1 << (j - 1))][j - 1]);
			else
				pre_calc[i][j] = pre_calc[i][j - 1];
		}
	}
	scanf("%d", &Q);
	for (int i = 0; i < Q; ++i) {
		int L, R;
		scanf("%d%d", &L, &R);
		if (R - L > 0) {
			int T = log(R - L) / log(2);
			printf("%d\n", min(pre_calc[L][T], pre_calc[R - (1 << T) + 1][T]));
		}
		else
			printf("%d\n", pre_calc[L][0]);
	}
}
```
