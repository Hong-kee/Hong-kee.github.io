---
title:  "[C++]프로그래머스 단어 변환"
excerpt: "[Level 3] DFS."

categories:
  - Algorithm
tags:
  - DFS
---
[문제](https://programmers.co.kr/learn/courses/30/lessons/43163)는 다음과 같다.

오늘은 프로그래머스 단어 변환 문제를 풀어보도록 하자. 단어의 갯수가 많지 않아서 DFS로 접근하며 풀 수 있는 문제였다. 모든 노드를 탐색하는데 

한 글자 차이가 나고 탐색하지 않은 곳을 탐색한다. 그 후 시작 단어를 교체해주고 카운트를 하나 늘려준다. 그리고 만일 같은 단어가 나오고

answer > cnt가 되면 answer값을 갱신해준다.

```c++
                                     [코드]
#include <string>
#include <vector>

using namespace std;

int answer = 987654321;
bool visit[50];

void dfs(string s, string e, vector<string>& words, int cnt) {
	if (s == e) {
		if (answer > cnt) {
			answer = cnt;
		}
		return;
	}
	for (int i = 0; i < words.size(); i++) {
		int check = 0;
		for (int j = 0; j < words[i].size(); j++) {
			if (s[j] != words[i][j]) {
				check++;
			}
		}
		if (check == 1 && !visit[i]) {
			visit[i] = true;
			dfs(words[i], e, words,  cnt + 1);
			visit[i] = false;
		}
	}
}

int solution(string begin, string target, vector<string> words) {
	dfs(begin, target, words, 0);
	if (answer == 987654321)answer = 0;
	return answer;
}
```
