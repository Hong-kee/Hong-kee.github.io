---
title:  "[C++]프로그래머스 짝지어 제거하기"
excerpt: "[Level 2] 스택 & 문자열"

categories:
  - Algorithm
tags:
  - 스택
  - 문자열
---
[문제](https://programmers.co.kr/learn/courses/30/lessons/12973)는 다음과 같다.

오늘은 프로그래머스 짝지어 제거하기를 풀어보도록 하자. 처음에 index를 비교해가며 만일 같으면 지우고 첫 번째 index로 돌아간 후, 다시 탐색하는 과정을 반복했더니 TLE가 나왔다. 만약 최악의 경우라면 O(N^2)의 시간복잡도가 나오게 되어 최대 입력인 100만의 제곱수의 시간이 나오게된다. 따라서 O(N)의 방법을 생각해보게 되었는데 바로 stack을 이용하는 방법이다.

1. 스택이 비어있으면 글자를 넣고
2. 위의 글자가 들어오려는 글자와 같으면 빼고
3. 같지 않다면 글자를 넣는다

위의 알고리즘 방식으로 O(N)의 시간복잡도를 가질 수 있었고 TLE를 피할 수 있었다.

```c++
                                     [코드]
#include <iostream>
#include <string>
#include <stack>

using namespace std;

int solution(string s)
{
    int answer = -1;//만일 다 지워진다면 1, 아니면 0
    stack<char>store_alpha;//입력 문자열의 문자 1개 씩을 저장하는 스택 선언
    
    for(int i = 0; i < s.length(); i++){//문자열 길이만큼 for문
        if(store_alpha.empty()) store_alpha.push(s[i]);// 만일 스택이 비어있으면 글자 쌓기
        else if(store_alpha.top() == s[i]) store_alpha.pop();//만일 스택의 위와 입력 글자가 같으면 pop해서 삭제
        else store_alpha.push(s[i]);//만일 다르면 글자 쌓기
    }
    
    if(store_alpha.empty())answer = 1;//비어있다면 다 삭제됐다는 얘기 -> 따라서 answer = 1
    else answer = 0;//아니면 0
    return answer;
}
```
