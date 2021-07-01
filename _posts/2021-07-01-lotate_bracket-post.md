---
title:  "[C++]프로그래머스 괄호 회전하기"
excerpt: "[Level 2] Stack & 문자열"

categories:
  - Algorithm
tags:
  - Stack
  - 문자열
---
[문제](https://programmers.co.kr/learn/courses/30/lessons/76502)는 다음과 같다.

오늘은 프로그래머스 괄호 회전하기를 풀어보도록 하자. 알맞은 괄호쌍을 찾는 알고리즘 문제에서 주어진 괄호를 회전하는 방식으로 문제가 더 추가되었다. 알맞은 괄호쌍을 찾는 문제는 stack을 이용하여 쉽게 풀 수 있다.

만일 stack의 맨 위 괄호가 들어올 괄호와 짝지어지지 않는 괄호이면 탈출하면 된다. 하지만 만일 열린 소괄호가 stack의 맨 위에 있다고 하자. 들어올 괄호가 열린 중괄호라면 스택에 쌓는다. 

왜냐하면 {()}의 예시가 있으므로 닫힌 괄호가 들어올 때 연산을 해야한다. 자세한 내용은 주석을 참고하자 ! :)

```c++
                                     [코드]
#include <iostream>
#include <string>
#include <vector>
#include <stack>

using namespace std;

int solution(string s) {
    int answer = 0; // 정답
    stack<char> store_brackets; //정확한 괄호가 맞는지 판단하기 위한 stack 선언
    
    for(int i = 0; i < s.length(); i++){ //괄호의 길이만큼 한 칸씩 회전
        for(int j = 0; j < s.length(); j++){
            if(store_brackets.empty()) { //비었으면 넣기
                store_brackets.push(s[j]); 
                continue;
            }
            
            if(store_brackets.top() == '['){ //만일 '['가 맨 위에 있고
                if(s[j] == ']') store_brackets.pop(); // 들어오는게 ']'면 사라져!
                else if(s[j] == '[' || s[j] == '{' || s[j] == '(') store_brackets.push(s[j]);// 열린괄호면 push
                else break;// 만일 닫힌 괄호인데 ')' or '}' 면 불완전 괄호이므로 탈출
            }
            //이하 같은 로직
            else if(store_brackets.top() == '{'){
                if(s[j] == '}') store_brackets.pop();
                else if(s[j] == '[' || s[j] == '{' || s[j] == '(') store_brackets.push(s[j]);
                else break;
            }
            else if(store_brackets.top() == '('){
                if(s[j] == ')') store_brackets.pop();
                else if(s[j] == '[' || s[j] == '{' || s[j] == '(') store_brackets.push(s[j]);
                else break;
            }
            else{
                break;
            }
        }
        //비었으면 ? answer 증가
        if(store_brackets.empty()) answer ++;
        
        //회전
        s.push_back(s[0]);
        s.erase(0, 1);
        //cout<<s<<'\n';
        //stack 비어주기
        while(!store_brackets.empty()) store_brackets.pop();
    }
    return answer;
}
```
