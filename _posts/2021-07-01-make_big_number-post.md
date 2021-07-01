---
title:  "[C++]프로그래머스 큰 수 만들기"
excerpt: "[Level 2] Greedy"

categories:
  - Algorithm
tags:
  - Greedy
---
[문제](https://programmers.co.kr/learn/courses/30/lessons/42883)는 다음과 같다.

오늘은 프로그래머스 큰 수 만들기를 풀어보도록 하자. 그리디 문제가 제일 어렵다. 처음에 완전 삽질했는데, 숫자 3개씩 짤라서 가장 작은 수를 없애며 k개 만큼 없앴을 때 종료한다 ! 라는 로직을 짰었다.

하지만 4441이고 k=2일 때 문제가 발생한다. 1이 지워지는건 확실하지만 나머지 1개는 어떤 것을 지울지 모른다. 그래서 한참을 더 생각하다가 도저히 아이디어가 떠오르지 않아 결국 구글링을 해서 이해했다.

우선 나와는 반대로 큰 수들을 먼저 뽑는 방식으로 접근한다. 그리고 for문을 돌려주는데 입력 값이 4177252841이고 k=4라고 하면, 결국 내가 출력할 문자열의 길이는 6이된다. 따라서 for문을 number.length() - k만큼 돌려주면 내가 출력할 문자열이 나온다.

이 for문 안에 큰 수들을 뽑을 수 있는 로직을 넣어줘야하는데 start부터 i + k만큼 돌려주면 된다.

```c++
                                     [코드]
#include <string>
#include <vector>

using namespace std;

string solution(string number, int k) {
    string answer = ""; //정답
    int idx = 0, start = 0;//index , start_index
    char num;
    
    for(int i = 0; i < number.length() - k; i++){
        num = number[start];
        idx = start;
        
        for(int j = start; j <= i + k; j++){
            if(num < number[j]){
                num = number[j];
                idx = j;
            }
        }
        answer += num;
        start = idx + 1;
    }
    
    return answer;
}
```
