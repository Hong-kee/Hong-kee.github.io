---
title:  "[C++]프로그래머스 자연수 뒤집어 배열로 만들기"
excerpt: "[Level 1] 구현 & 문자열"

categories:
  - Algorithm
tags:
  - 구현
  - 문자열
---
[문제](https://programmers.co.kr/learn/courses/30/lessons/12932)는 다음과 같다.

오늘은 프로그래머스 자연수 뒤집어 배열로 만들기를 풀어보도록 하자. int to string을 이용하는 문제이다. 다른 문제들과 마찬가지로 to_string함수를 쓰면 편리하다. answer 벡터가 int인건 주의하고 아스키코드표를 이용하여 변환시켜주도록 하자 : )
```c++
                                     [코드]
#include <string>
#include <vector>

using namespace std;

vector<int> solution(long long n) {
    vector<int> answer;//정답을 저장하는 벡터
    string number = to_string(n);//n을 문자열로 바꾸어 저장하기 위한 string class
    
    for(int i = number.length() - 1; i >= 0; i--){
        answer.push_back(number[i] - '0');//아스키코드를 이용하여 int형으로 저장
    }
    return answer;
}
```
