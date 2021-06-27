---
title:  "[C++]프로그래머스 정수 내림차순으로 배치하기"
excerpt: "[Level 1] 구현 & 문자열 & Sort"

categories:
  - Algorithm
tags:
  - 구현
  - 문자열
  - Sort
---
[문제](https://programmers.co.kr/learn/courses/30/lessons/12933)는 다음과 같다.

오늘은 프로그래머스 정수 내림차순으로 배치하기를 풀어보도록 하자. long long을 string으로 변환시켜준 후, sort함수로 내림차순을 해준다. 그 후 stol로 변환하여 return하면 끗 : )

```c++
                                     [코드]
#include <string>
#include <algorithm>

using namespace std;

long long solution(long long n) {
    string convert_string_answer = to_string(n);//n을 문자열로 저장하기 위한 string class
    sort(convert_string_answer.rbegin(), convert_string_answer.rend());
    return stol(convert_string_answer);
}
```
