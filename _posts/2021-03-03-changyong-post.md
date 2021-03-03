---
title:  "[C++]SW Expert Academy 창용 마을 무리의 갯수"
excerpt: "[D4] DFS."

categories:
  - Algorithm
tags:
  - DFS
---
[문제](https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AWngfZVa9XwDFAQU)는 다음과 같다.

오늘은 SW Expert Academy 창용 마을 무리의 갯수 문제를 풀어보도록 하자. SWEA의 문제는 테스트케이스를 정해놓고 돌리기 때문에 초기화에 신경을 잘 써주어야한다.

인접행렬을 통하여 그룹의 갯수를 찾는 문제였다. 즉, UnionFind 문제이다. DFS를 통하여 방문체크를 하며 만일 방문체크가 된 곳을 다시 간다면 return해주는 방식으로 코드를 작성했다.

예를 들어, N=10, M=3, 1 2, 1 3, 1 4의 케이스가 들어왔다면 {1,2,3,4}, {5}, {6}, {7}, {8}, {9}, {10}으로 그룹이 만들어지고 답은 7개가 된다.

```c++
                                     [코드]
#include <iostream>
using namespace std;

bool visit[101];
bool map[101][101];
int answer = 0, num = 0, T, N, M, a, b;//T=테스트케이스 N=사람 수 M=관계 수;

void Init() { //초기화
	for (int i = 1; i <= N; i++) {
		visit[i] = false;
	}
	for (int i = 1; i <= N; i++) {
		for (int j = 1; j <= N; j++) {
			map[i][j] = false;
		}
	}
}

void dfs(int idx) {//디엪스
	if (visit[idx]) {
		return;
	}
	visit[idx] = true;
	for (int i = 1; i <= N; i++) {
		if (map[idx][i]) {
			dfs(i);
		}
	}
}

int main() {
	ios::sync_with_stdio(false);
	cin.tie(0);

	cin >> T;

	while (T--) {
		answer = 0;
		cin >> N >> M;
		for (int i = 0; i < M; i++) {//인접행렬 맹글기
			cin >> a >> b;
			map[a][b] = true;
			map[b][a] = true;
		}

		for (int i = 1; i <= N; i++) {
			if (!visit[i]) {//사람 체크 안 했으면 사이클 돌리기
				answer++;
				dfs(i);
			}
		}
		cout << '#' << ++num << ' ' << answer << '\n';
		Init();//초기화
	}
}
```
