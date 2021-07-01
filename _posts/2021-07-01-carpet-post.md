---
title:  "[C++]프로그래머스 카펫"
excerpt: "[Level 2] Searching"

categories:
  - Algorithm
tags:
  - Searching
---
[문제](https://programmers.co.kr/learn/courses/30/lessons/42842)는 다음과 같다.

오늘은 프로그래머스 카펫을 풀어보도록 하자. 완전 탐색 문제이다. 약수들을 뽑아서 (가로 - 2) * (세로 - 2)의 값이 노란 카펫의 갯수와 같으면 answer 벡터에 넣어주는 식으로 풀었다.

```c++
                                     [코드]
#include <string>
#include <vector>

using namespace std;

vector<int> answer;//정답

void FindSize(int w, int h, int yellow){//가로,세로 찾는 함수
    //w = 가로, h = 세로
    if((w - 2) * (h - 2) == yellow) { //만일 갯수를 찾았다면 ?
        answer.push_back(w);
        answer.push_back(h);
    }
}

vector<int> solution(int brown, int yellow) {
    int total_carpet = brown + yellow;
    
    //약수 찾기
    for(int i = 2; i <= total_carpet; i++){
        if(total_carpet % i == 0){ //만일 약수라면 ?
            FindSize(total_carpet / i, i, yellow);//가로, 세로 찾는 함수 작동
            if(answer.size() != 0)break;//만일 찾았으면 ? 탈출
        }
    }
    return answer;
}
```
