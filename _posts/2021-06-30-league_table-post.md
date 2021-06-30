---
title:  "[C++]프로그래머스 예상 대진표"
excerpt: "[Level 2] Math"

categories:
  - Algorithm
tags:
  - Math
---
[문제](https://programmers.co.kr/learn/courses/30/lessons/12985#)는 다음과 같다.

오늘은 프로그래머스 예상 대진표를 풀어보도록 하자. 대진표가 주어지는데 a번과 b번은 만날 때까지 이긴다는 가정하에 몇 번의 대전을 해야할까? 라는 문제였다. 수학적인 문제였고 입력 값이 2의 지수승으로 주어지기 때문에 예외처리에 대한 짐이 조금 덜어졌다.

while문을 돌리면서 a의 값과 b의 값을 홀,짝에 관해 처리하며 갱신해주고 돌리다가 만일 a와 b의 값이 같아진다면, 종료하면 된다! : )

```c++
                                     [코드]
#include <iostream>
#include <cmath>
using namespace std;

int solution(int n, int a, int b)
{
    int answer = 0; //정답
    
    while(a != b){
        //홀,짝처리 둘 다 가능
        a = a / 2 + a % 2; 
        b = b / 2 + b % 2;
        answer++;
        
        if(a == b)break; //만일 같다면 탈출
    }
    return answer;
}
```
