---
title:  "[C++]프로그래머스 이상한 문자 만들기"
excerpt: "[Level 1] 구현 & 문자열"

categories:
  - Algorithm
tags:
  - 구현
  - 문자열
---
[문제](https://programmers.co.kr/learn/courses/30/lessons/12930)는 다음과 같다.

오늘은 프로그래머스 이상한 문자 만들기를 풀어보도록 하자. 문자열 파싱 문제이다. 공백을 기준으로 단어의 인덱스를 판별한 후, 단어의 인덱스가 짝수면 대문자로 변환, 홀수면 소문자로 변환 후 answer에 추가하고 출력하면 된다 !
```c++
                                     [코드]
#include <string>
#include <algorithm>

using namespace std;

string solution(string s) {
    int index = 0;//각 단어별 인덱스
    string answer = "";//정답
    
    for(int i = 0; i < s.length(); i++){//입력 글자만큼 for문
        if(s[i] == ' '){//만일 입력 글자가 공백이라면
            answer += " ";//정답에 공백추가 후 단어의 인덱스 0으로 초기화
            index = 0;
            continue;
        }
        else{
            if(index % 2 == 0) answer += toupper(s[i]); //단어의 인덱스가 짝수 -> 대문자 변환 후 정답에 추가
            else answer += tolower(s[i]);// 단어의 인덱스가 홀수 -> 소문자 변환 후 정답에 추가
            index ++;// 단어의 인덱스 1증가
        }
    }
    return answer;
}
```
