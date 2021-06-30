---
title:  "[C++]프로그래머스 소수 찾기"
excerpt: "[Level 2] DFS & 문자열"

categories:
  - Algorithm
tags:
  - DFS
  - 문자열
---
[문제](https://programmers.co.kr/learn/courses/30/lessons/42839)는 다음과 같다.

오늘은 프로그래머스 소수 찾기를 풀어보도록 하자. DFS를 이용하여 문자열을 만드는데, 후에 값을 처리하는 과정 때문에 string to int 형변환을 해주어야했다. DFS를 이용하여 사용한 개념은 '부분집합' 이다.

왜냐면 만일 주어진 문자열이 "123"라고 하자. 그럼 나올 수 있는 숫자는 1, 2, 3, 12, 13, 21, 23, 31, 32로 9가지가 나온다. 문자열을 만들 때는 겹치는 index는 처리해주면 안되기 때문에 따로 check배열을 두어 중복을 피해주었다.

그 후 string to int 변환을 하여 소수인지 판별해주면 된다 ! 그리고 만약 카운트했던 수라면 check_number을 통해 중복처리를 빼주면 된다!

```c++
                                     [코드]
#include <iostream>
#include <string>
#include <vector>

using namespace std;

bool check_number[10000000];//숫자체크 배열 선언(중복처리)
bool check[8];//DFS용 글자 index처리 배열
int answer = 0;//정답
string temp_number = "";//임시 숫자 string

bool isPrime(string temp_number){
    //cout<<temp_number<<'\n'; ---출력
    
    if(temp_number[0] == '0') return false; //만일 첫 글자가 0이면 false
    int number = stoi(temp_number); // string to int
    if(check_number[number] || number == 1) return false; //만일 이미 체크된 것이면 or 숫자가 1이면(소수가 아니므로) false
    
    check_number[number] = true;//숫자 체크
    for(int i = 2; i <= number / 2; i++){ // Prime number checking
        if(number % i == 0) return false; //not Prime number
    }
    return true;
}

void Pick_Numbers(string numbers){
    if(temp_number.length() != 0 && (temp_number.length() <= numbers.length())){ //만일 길이 0이 아니고 같거나 작으면 ?
        if(isPrime(temp_number)){ //소수면 ?
            answer++;// 정답 ++;
        }
    }
    for(int i = 0; i < numbers.length(); i++){
        if(check[i])continue; // 이미 처리된 index면 ? continue
        check[i] = true; //index 처리
        temp_number += numbers[i];//문자열 추가
        Pick_Numbers(numbers); //재귀
        check[i] = false;//index 처리 해제
        temp_number.pop_back();//문자열 삭제
    }
}

int solution(string numbers) {
    Pick_Numbers(numbers);//숫자를 만드는 조합식
    return answer;
}
```
