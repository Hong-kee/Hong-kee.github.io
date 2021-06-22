---
title:  "[C++]프로그래머스 약수의 개수와 덧셈"
excerpt: "[Level 1] 구현."

categories:
  - Algorithm
tags:
  - 구현
---
[문제](https://programmers.co.kr/learn/courses/30/lessons/77884)는 다음과 같다.

오늘은 프로그래머스 약수의 개수와 덧셈을 풀어보도록 하자.

... 자세한 설명은 주석에서 !

```c++
                                     [코드]
using namespace std;

bool FindDivisor(int num, int divisor_count){
    for(int i=1;i<=num;i++){
      //만일 i로 나누어 떨어진다면 약수이다.  
      if(num % i == 0){
            divisor_count++;
        }
    }
    //약수의 갯수가 짝수라면 ? 
    if(divisor_count % 2 == 0){
        return true;
    }
    return false;
}

int solution(int left, int right) {
    //정답
    int answer = 0;
    //left부터 right까지 약수의 갯수 판별
    for(int i=left;i<=right;i++){
        //만일 약수의 갯수가 짝수면
        if(FindDivisor(i,0)){
            answer+=i;
        }
        //홀수면
        else{
            answer-=i;
        }
    }
    
    return answer;
}
```
