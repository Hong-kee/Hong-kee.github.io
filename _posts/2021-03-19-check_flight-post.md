---
title:  "[C++]프로그래머스 입국심사"
excerpt: "[Level 3] Binary Search."

categories:
  - Algorithm
tags:
  - Binary Search
---
[문제](https://programmers.co.kr/learn/courses/30/lessons/43238)는 다음과 같다.

오늘은 프로그래머스 입국심사 문제를 풀어보도록 하자. 이분탐색 문제라는데 이분탐색이라는 감도 잡히지 않았다. 데이터의 범위를 보고 dp를 의심해봤지만 dp의 힌트도 보이지 않았다.

이분탐색으로 어떻게 접근할 수 있을까에 대한 고민을 하다가 해설을 봤다. 이분탐색을 하려면 우선 범위 설정이 되어야 하고, 오름차순 정렬이 되어있어야 한다. 범위 설정을 가능한 최솟값부터 가능한 최댓값으로 설정해주었다. 

우선 최솟값start는 가장 작게 들어올 수 있는 최솟값인 1로 시작했다. 그리고 최댓값end는 가장 크게 들어올 수 있는 최악의 값인 가장 긴 입국심사시간 * 사람 수로 설정했다.

즉, 만일 6명이고 각 입국심사시간이 7 10이면 start = 1, end = 6 * 10 = 60으로 설정해주고 mid값을 갱신해가면서 문제를 해결했다.

근데 여기서 갱신조건을 설정해주어야 한다. 즉, start와 end가 언제 바뀌고 answer값은 언제 갱신되는지 파악을 해야한다.

생각해보면 사람의 수를 비교하면 된다. 만일 6명이고 7 10이 입국심사의 시간이라고 하자. 처음 mid값은 1과 60의 절반인 30이 되겠고 30/7 = 4, 30/10 = 3으로 총 7명의 사람을 체크할 수 있는 것이다.

n=6이니 7명의 사람을 체크할 수 있다는 것은 조건이 성립된다. 따라서 answer = mid로 설정하고 7명은 계산하기 충분하니 end = mid-1로 설정해주고 범위를 서서히 좁혀나가면 되겠다.

그리고 주의해야할 점이 또 있다. 바로 ___자료형___ 이다. long long 타입의 변수를 받을 땐 꼭 long long과 계산을 해주도록 하자.

이 부분 때문에 로직을 짜고도 테스트8번에서 계속 막혔다.

```c++
                                     [코드]
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

long long solution(int n, vector<int> times) {
	sort(times.begin(), times.end());
	long long back = times[times.size() - 1];
	long long cnt = n;
	long long answer = back * cnt, start = 1, end = back * cnt;
	while (start <= end) {
		long long mid = (start + end) / 2, temp = 0;
		for (long long i = 0; i < times.size(); i++) {
			temp += mid / times[i];
		}
		if (temp < cnt) {
			start = mid + 1;
		}
		else {
			answer = mid;
			end = mid - 1;
		}
	}
	return answer;
}
```
