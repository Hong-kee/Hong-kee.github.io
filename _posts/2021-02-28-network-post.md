---
title:  "[C++]프로그래머스 네트워크"
excerpt: "[Level 3] DFS."

categories:
  - Algorithm
tags:
  - DFS
---
[문제](https://programmers.co.kr/learn/courses/30/lessons/43162)는 다음과 같다.

오늘은 프로그래머스 네트워크 문제를 풀어보도록 하자. DFS문제로 그룹의 갯수를 리턴하는 문제이다. 각 노드를 탐색하며 탐색한 노드는 0으로 만들어서 

방문처리를 해주었다. 탐색했던 노드를 가서 또 연결을 확인하려 한다면 return false로 카운트하지 않았다.
      

```c++
                                     [코드]
#include <string>
#include <vector>

using namespace std;
bool dfs(int idx, vector<vector<int>>& computers) {
	if (!computers[idx][idx]) return false;

	computers[idx][idx] = 0;
	for (int i = 0; i < computers.size(); i++) {
		if (computers[idx][i] == 1) {
			dfs(i, computers);
		}
	}
	return true;
}

int solution(int n, vector<vector<int>> computers) {
	int answer = 0;

	for (int i = 0; i < n; i++) {
		if (computers[i][i] && dfs(i, computers)) answer++;
	}
	return answer;
}
```
