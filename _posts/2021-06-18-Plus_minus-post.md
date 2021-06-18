---
title:  "[C++]프로그래머스 음양 더하기"
excerpt: "[Level 1] Greedy."

categories:
  - Algorithm
tags:
  - Greedy
---
[문제](https://programmers.co.kr/learn/courses/30/lessons/76501)는 다음과 같다.

오늘은 프로그래머스 음양 더하기 문제를 풀어보도록 하자.

.. 자세한 내용은 생략하기로 하자..

```c++
                                     [코드]
#include <string>
#include <vector>

using namespace std;

int solution(vector<int> absolutes, vector<bool> signs) {
    int answer=0;
    
    for(int i=0;i<absolutes.size();i++){
        //false
        if(!signs[i]){
            answer -= absolutes[i];
        }
        //true
        else{
            answer += absolutes[i];
        }
    }
    return answer;
}
```
