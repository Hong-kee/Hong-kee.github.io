---
title:  "[C++]프로그래머스 여행 경로"
excerpt: "[Level 3] DFS."

categories:
  - Algorithm
tags:
  - DFS
---
[문제](https://programmers.co.kr/learn/courses/30/lessons/43164)는 다음과 같다.

오늘은 프로그래머스 여행 경로 문제를 풀어보도록 하자. 반례 덕분에 꽤나 애먹었던 문제였다. 우선 정렬을 하여 알파벳 순서대로 놓았다. 그 후의 풀이는 다음과 같다.

1. ICN이 나오면 dfs를 돌린다.
2. 그 후 start를 도착지점으로 초기화 시킨 후 각 원소의 시작지점 == start이면 visit[idx]를 방문처리 해주고 dfs를 돌려주는 방식으로 했다.
3. 백트래킹으로는 모든 지점을 돌았을 때 재귀로 쌓였던 스택들은 돌 필요가 없으므로 flag = true로 해주고 마지막 지점을 answer벡터에 푸쉬해주었다.

*여기서 문제는 알파벳 순서대로 갔다고 해도 모든 경유지를 찍지 못하는 경우가 발생할 수 있다는 점이다.

따라서 만일 dfs함수 안에서의 for문을 다 돌려도 안된다면 answer벡터에 푸쉬해줬던 원소를 빼주고 방문처리했던 visit[idx]=false 처리 해주어야 한다. --> 애먹은 부분(이 부분이 처리가 안되면 1,2번 틀립니다.)

위 문제를 통해서 TC의 중요성을 알았고 다양한 방면에서 생각해야겠다는 것을 배웠다.
```c++
                                     [코드]
#include <string>
#include <vector>
#include <algorithm>
using namespace std;

vector<string> answer;
string start;
bool visit[10001];
bool flag;

void dfs(int idx, vector<vector<string>>& tickets) {
	visit[idx] = true;
	answer.push_back(tickets[idx][0]);
	start = tickets[idx][1];

	if (tickets.size() == answer.size()) {
		answer.push_back(start);
		flag = true;
		return;
	}
	for (int i = 0; i < tickets.size(); i++) {
		if (!visit[i] && start == tickets[i][0]) {
			visit[i] = true;
			dfs(i, tickets);
			start = tickets[idx][1];
		}
		if (flag) {
			return;
		}
	}
	answer.pop_back();
    visit[idx] = false;
}


vector<string> solution(vector<vector<string>> tickets) {
        sort(tickets.begin(), tickets.end());
    	for (int i = 0; i < tickets.size(); i++) {
		if (!visit[i] && tickets[i][0] == "ICN") {
            dfs(i, tickets);
		}
	}
    return answer;
}
```
