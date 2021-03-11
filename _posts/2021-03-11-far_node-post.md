---
title:  "[C++]프로그래머스 가장 먼 노드"
excerpt: "[Level 3] BFS."

categories:
  - Algorithm
tags:
  - BFS
  - Graph
---
[문제](https://programmers.co.kr/learn/courses/30/lessons/49189)는 다음과 같다.

오늘은 프로그래머스 가장 먼 노드 문제를 풀어보도록 하자. BFS문제로 1로부터 가장 멀리 있는 노드의 갯수를 찾는 것이다. bfs함수를 돌리면서 가장 마지막에 저장되어 있는 노드의 갯수는 결국 queue가 다 비워지기 전의 사이즈 이므로 size_of_Q 값을 리턴해주면 되겠다.

state벡터를 따로 두었는데 연결되어있는 노드들을 파악하기 위해서 설정해둔 것이다. 예를 들어 1과 2가 연결되어 있다면 state[1]에 2 값을 넣고, state[2]에 1값을 넣어서 양방향이라는 것을 체크해주었다.

```c++
                                     [코드]
#include <string>
#include <queue>
#include <vector>
using namespace std;

bool visit[20001];
vector<int>state[20001];
queue<int>Q;

int bfs() {
	Q.push(1);
    int size_of_Q;
	while (!Q.empty()) {
		size_of_Q = Q.size();
		for (int i = 0; i < size_of_Q; i++) {
			int cur = Q.front();
			Q.pop();

			visit[cur] = true;
			for (int j = 0; j < state[cur].size(); j++) {
				if (!visit[state[cur][j]]) {
					Q.push(state[cur][j]);
					visit[state[cur][j]] = true;
				}
			}

		}
	}
	return size_of_Q;
}

int solution(int n, vector<vector<int>> edge) {
	for (int i = 0; i < edge.size(); i++) {
		state[edge[i][0]].push_back(edge[i][1]);
		state[edge[i][1]].push_back(edge[i][0]);
	}
	int answer = bfs();

	return answer;
}
```
