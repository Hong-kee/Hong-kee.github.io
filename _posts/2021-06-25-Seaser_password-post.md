---
title:  "[C++]프로그래머스 시저 암호"
excerpt: "[Level 1] 구현 & 문자열"

categories:
  - Algorithm
tags:
  - 구현
  - 문자열
---
[문제](https://programmers.co.kr/learn/courses/30/lessons/12926)는 다음과 같다.

오늘은 프로그래머스 시저 암호를 풀어보도록 하자. 아스키코드를 이용하여 푸는 문제이다. 우선 소문자인지 대문자인지 판별을 하고 'z' or 'Z'를 벗어나는지 판별을 한 후 'a' - 1부터 n만큼 이동시켜주면 된다.

```c++
                                     [코드]
#include <string>

using namespace std;

string solution(string s, int n) {
    string answer = "";
    for(int i = 0; i < s.length(); i++){
        if(s[i] == ' '){ //만일 빈칸일 경우, 정답에 빈칸 추가 후 continue
            answer += " ";
            continue;
        }
        //만일 대문자인데 'Z'를 넘어가거나, 소문자인데 'z'를 넘어가면
        if(s[i] + n > 90 && (s[i] >= 65 && s[i] <= 90)|| s[i] + n > 122 && (s[i] >= 97 && s[i] <= 122)){
            answer += s[i] - 26 + n;//'a' - 1또는 'A' - 1에서 시작해서 n만큼 움직인 후 정답에 추가
        }
        else answer += s[i] + n;//아닐경우 그냥 n만큼 움직인 후 정답에 추가
    }
    return answer;
}
```
