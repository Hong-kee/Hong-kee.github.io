---
title:  "[C++]프로그래머스 3진법 뒤집기"
excerpt: "[Level 1] 구현"

categories:
  - Algorithm
tags:
  - 구현
---
[문제](https://programmers.co.kr/learn/courses/30/lessons/68935)는 다음과 같다.

오늘은 프로그래머스 3진법 뒤집기을 풀어보도록 하자. 우선 3진법을 만드는 작업을 해야한다. 3진법을 만들기 위해 Modulation연산을 하고 나머지를 ternary 벡터에 넣어준다. 만일, 몫이 3 미만이면 몫을 넣어주고 함수를 끝낸다.

그리고 10진법으로 바꿔주는 연산을 하면 끝! : )

```c++
                                     [코드]
#include <string>
#include <vector>
#include <cmath>

using namespace std;

int solution(int n) {
    //정답
    int answer = 0;
    //3진법 설정
    vector<int>ternary;
    
    //n이 3보다 작을 때 까지
    while(1){
        if(n<3){
            ternary.push_back(n);
            break;
        }
        else{
            ternary.push_back(n%3);
            n /= 3;
        }
    }
    //10진법 변환
    for(int i=ternary.size() - 1;i>=0;i--){
        answer += ternary[i] * pow(3, ternary.size() - 1 - i);
    }
    return answer;
}
```
