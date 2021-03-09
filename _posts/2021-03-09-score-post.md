---
title:  "[C++]SW Expert Academy 가능한 시험 점수"
excerpt: "[D4] Greedy"

categories:
  - Algorithm
tags:
  - Greedy
---
[문제](https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AWHPkqBqAEsDFAUn)는 다음과 같다.

오늘은 SW Expert Academy 가능한 시험 점수 문제를 풀어보도록 하자. 처음에 조합을 생각하고 dfs로 접근하려 했다. 하지만 Data가 100개가 주어질 수 있기 때문에 O(2^100)이라는 어마무시한 시간복잡도를 가질 수 있게 된다. 

따라서 다른 방법으로 풀어야 하는데 값을 입력받고 원래 있던 시험점수의 합을 한 다음 저장되어 있던 벡터에 존재하냐 하지 않느냐를 판단해주면 된다. visit배열로 존재하는 값을 처리해주었고 2중 for문으로 처리해줌으로써

시간복잡도를 O(N^2)으로 낮출 수 있었다. 위 문제로 너무 탐색문제에 얽매인 나를 볼 수 있었다. 다르게 생각하는 법을 길러야겠다.

```c++
                                     [코드]
#include <iostream>
#include <algorithm>
#include <vector>
using namespace std;

bool visit[10001];
int N, sum = 0;
vector<int>answer;

void Init() {
	for (int i = 0; i <= 10000; i++) {
		visit[i] = false;
	}
	answer.clear();
}

int main() {
	ios::sync_with_stdio(false);
	cin.tie(0);

	int T, num = 0, temp;

	cin >> T;

	while (T--) {
		Init();
		cin >> N;
		answer.push_back(0);
		visit[0] = true;

		for (int i = 0; i < N; i++) {
			cin >> temp;
			int size_of_answer = answer.size();

			for (int j = 0; j < size_of_answer; j++) {
				if (!visit[temp + answer[j]]) {
					answer.push_back(temp + answer[j]);
					visit[temp + answer[j]] = true;
				}
			}
		}
		cout << "#" << ++num << " " << answer.size() << '\n';
	}
}
```
