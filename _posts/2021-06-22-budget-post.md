---
title:  "[C++]프로그래머스 예산"
excerpt: "[Level 1] Sort."

categories:
  - Algorithm
tags:
  - Sort
---
[문제](https://programmers.co.kr/learn/courses/30/lessons/12982)는 다음과 같다.

오늘은 프로그래머스 예산을 풀어보도록 하자. 단순 정렬문제이다. 정렬을 하고 예산 내에 있는 부서면 answer++, 아니면 break를 하여 answer값을 출력해주면 된다.

```c++
                                     [코드]
#include <vector>
#include <algorithm>

using namespace std;

int solution(vector<int> d, int budget) {
    //정답
    int answer = 0;
    //오름차순
    sort(d.begin(),d.end());
    //지원 고고씽
    for(int i=0;i<d.size();i++){
        if(d[i]<=budget){
            answer++;
            budget-=d[i];
        }
        else{
            break;
        }
    }
    
    return answer;
}
```
