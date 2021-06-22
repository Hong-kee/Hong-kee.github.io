---
title:  "[C++]프로그래머스 실패율"
excerpt: "[Level 1] 구현 & Sort."

categories:
  - Algorithm
tags:
  - 구현
  - Sort
---
[문제](https://programmers.co.kr/learn/courses/30/lessons/42889)는 다음과 같다.

오늘은 프로그래머스 실패율을 풀어보도록 하자. 구현과 정렬을 해야하는 문제였다. 그리고 벡터를 pair로 설정하여 second를 기준으로 first를 오름차순으로 정렬하는 compare함수를 세팅해줘야했다.

만일 실패율이 같을 때 스테이지의 숫자가 작은 것이 앞으로 오도록 compare함수를 만들어주는 것이 Point이다. : )

```c++
                                     [코드]
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

//내림차순 설정(실패율을 기준으로)
bool compare(pair<int,double> &p1, pair<int,double> &p2){
    if(p1.second == p2.second){
        return p1.first < p2.first;
    }
    return p1.second > p2.second;
}

vector<int> solution(int N, vector<int> stages) {
    //정답
    vector<int> answer;
    //stage와 실패율을 담는 벡터
    vector<pair<int,double>> failure_information(N+1);
    
    //실패 명수 카운팅
    for(int i=0;i<stages.size();i++){
        failure_information[stages[i]].first++;
    }
    
    //초기 명수 설정
    int challengers = stages.size();
    
    //실패율 설정
    for(int i=1;i<=N;i++){
        if(challengers == 0){
            failure_information[i].second = 0;
            continue;
        }
        failure_information[i].second = (double)failure_information[i].first / challengers;
        challengers -= failure_information[i].first;
    }
    
    //index설정
    for(int i=1;i<=N;i++){
        failure_information[i].first = i;
    }
    //정렬
    sort(failure_information.begin() + 1, failure_information.end(), compare);
    
    //answer에 push
    for(int i=1;i<=N;i++){
        answer.push_back(failure_information[i].first);
    }
    return answer;
}
```
