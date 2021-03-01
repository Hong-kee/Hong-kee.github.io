---
title:  "[C++]프로그래머스 정수 삼각형"
excerpt: "[Level 3] Dynamic Programming."

categories:
  - Algorithm
tags:
  - Dynamic Programming
---
[문제](https://programmers.co.kr/learn/courses/30/lessons/43105)는 다음과 같다.

오늘은 프로그래머스 정수 삼각형 문제를 풀어보도록 하자. 우선 오늘은 3.1절이다. 우리는 독립운동가 분들 덕분에 현재의 삶을 살고 있다. 감사하는 마음으로 살겠습니다.

이번 문제는 DP문제로 0~triangle크기만큼 내려오면서 누적합이 가장 큰 값을 출력하는 것이다.

테두리 부분은 중복으로 계산되지 않기 때문에 그냥 누적합을 해주면 되지만 계산이 중첩되는 구간이 있어서 인덱스별로 처리를 해주어야 했다.

현재의 값에서 그 위 인덱스 양쪽 값 중 큰 것을 누적합해주면 된다. 그 후 최댓값을 찾아 return하면 끝이다.


```c++
                                     [코드]
#include <string>
#include <vector>
#include <algorithm>
using namespace std;

int solution(vector<vector<int>> triangle) {
	int answer = -1;

	for (int i = 1; i < triangle.size(); i++) {
		for (int j = 0; j < triangle[i].size(); j++) {
			if (j == 0) {
				triangle[i][j] += triangle[i - 1][0];
			}
			else if (j == triangle[i].size() - 1) {
				triangle[i][j] += triangle[i - 1][i - 1];
			}
			else {
				triangle[i][j] += max(triangle[i - 1][j - 1], triangle[i - 1][j]);
			}
		}
	}

	for (int i = 0; i < triangle.size(); i++) {
		if (answer < triangle[triangle.size() - 1][i]) {
			answer = triangle[triangle.size() - 1][i];
		}
	}
	return answer;
}
```
