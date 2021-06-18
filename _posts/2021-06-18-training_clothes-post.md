---
title:  "[C++]프로그래머스 체육복"
excerpt: "[Level 1] Greedy."

categories:
  - Algorithm
tags:
  - Greedy
---
[문제](https://programmers.co.kr/learn/courses/30/lessons/42862)는 다음과 같다.

오늘은 프로그래머스 체육복 문제를 풀어보도록 하자. Level 1 문제로 오랜만에 Greedy문제를 풀다보니 초반에 좀 멍했다. 아무래도 요즘 알고리즘 공부를 안 한 벌을 받고 있는 것 같다. ㅠㅠ.. 항상 많이 하려고 하지 말고 꾸준히 조금씩 한다는 마인드로 해야겠다. : )

여튼! 위 문제는 체육복을 도난당한 친구들을 구제해주는 문제이다. 아래 주석을 참고하자 ! 어렵지 않다 !

```c++
                                     [코드]
#include <string>
#include <vector>

using namespace std;

int solution(int n, vector<int> lost, vector<int> reserve) {
    int answer=0;
    //n명의 체육복 갯수를 1로 세팅
    vector<int> student_clothes(n, 1);
    //여분의 체육복을 가진 학생들 +1씩 해줌
    for(int i=0;i<reserve.size();i++){
        student_clothes[reserve[i]-1]++;
    }
    //도난당한 학생들은 -1씩해줌
    for(int i=0;i<lost.size();i++){
        student_clothes[lost[i]-1]--;
    }
    //n번을 돌면서
    for(int i=0;i<n;i++){
        //만일 체육복이 없고 앞 친구는 2벌이면, 본인 +1/앞 친구-1
        if(i>0 && student_clothes[i] == 0 && student_clothes[i-1] == 2){
            student_clothes[i]++;
            student_clothes[i-1]--;
        }
        //만일 체육복이 없고 뒷 친구는 2벌이면, 본인 +1/뒷 친구 -1
        else if(i<n-1 && student_clothes[i] == 0 && student_clothes[i+1] == 2){
            student_clothes[i]++;
            student_clothes[i+1]--;
        }
    }
    //0벌인 친구들 제외한 명수 구하기
    for(int i=0;i<n;i++){
        if(student_clothes[i] != 0)answer++;
    }
    return answer;
}
```
