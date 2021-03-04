---
title:  "[C++]SW Expert Academy 격자판의 숫자 이어 붙이기"
excerpt: "[D4] DFS & Set"

categories:
  - Algorithm
tags:
  - DFS
  - Set
---
[문제](https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AV7I5fgqEogDFAXB)는 다음과 같다.

오늘은 SW Expert Academy 격자판의 숫자 이어 붙이기 문제를 풀어보도록 하자. 4 by 4의 격자판이 있다. 문제를 해석해보면 _임의의 격자판에서 시작한다._ 라고 했으므로 main문에서 총 16번의 dfs를 

돌려주어야 한다. 그리고 숫자가 겹칠 수 있다. 따라서 vector Container대신 set Container를 사용하여 겹치는 것을 처리해주었다. 다시 문제로 돌아가면 갔던 곳을 재방문 할 수 있다고 했으므로

방문처리를 해주지 않고 idx범위만 판단하여 dfs를 돌려야하는 것을 알 수 있다.

```c++
                                     [코드]
#include <iostream>
#include <set>
#include <string>
using namespace std;

char map[4][4];
int dir[4][2] = { {-1,0},{0,1},{1,0},{0,-1} };
set<string>v;

void dfs(int y, int x, string s) {
	if (s.length() == 7) {
		v.insert(s);
		return;
	}
	s += map[y][x];
	for (int i = 0; i < 4; i++) {
		int my = y + dir[i][0];
		int mx = x + dir[i][1];

		if (my >= 0 && mx >= 0 && my < 4 && mx < 4) {
			dfs(my, mx, s);
		}
	}
}

int main() {
	ios::sync_with_stdio(false);
	cin.tie(0);

	int T, num = 0;

	cin >> T;

	while (T--) {
		for (int i = 0; i < 4; i++) {
			for (int j = 0; j < 4; j++) {
				cin >> map[i][j];
			}
		}
		for (int i = 0; i < 4; i++) {
			for (int j = 0; j < 4; j++) {
				dfs(i,j,"");
			}
		}
		cout << '#' << ++num << ' ' << v.size() << '\n';
		v.clear();
	}
}
```
