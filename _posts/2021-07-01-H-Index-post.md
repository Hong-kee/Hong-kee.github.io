---
title:  "[C++]프로그래머스 H-Index"
excerpt: "[Level 2] Sort"

categories:
  - Algorithm
tags:
  - Sort
---
[문제](https://programmers.co.kr/learn/courses/30/lessons/42747)는 다음과 같다.

오늘은 프로그래머스 H-Index를 풀어보도록 하자. 원래는 sort내장함수로 풀 수 있는 문제인데 데이터 갯수가 적다보니 카운팅소트로 풀게되었다. 만일 인용 횟수가 3이라고 하면 3이하의 인덱스에 다 1씩 더해주고

마지막 answer값을 출력할 때는 인덱스와 인용 값을 비교하여 인용 값이 크거나 같으면 정답처리를 해주었다 :)

```c++
                                     [코드]
#include <string>
#include <vector>

using namespace std;

//데이터 갯수가 작으므로 카운팅소트로 해결

int solution(vector<int> citations) {
    int answer = 0;//정답
    int citation[10001] = {0, }; //카운팅 초기화
    
    for(int i = 0; i < citations.size(); i++){
        for(int j = citations[i]; j > 0; j--){
            citation[j]++; //카운팅소트
        }
    }
    
    for(int i = 1; i <= 10001; i++){
        if(i <= citation[i]){ //만일 인용횟수가 인덱스보다 크거나 같다면 ?
            answer = i; //정답!
        }
    }
    return answer;
}
```
