---
title:  "[C++]프로그래머스 로또의 최고순위와 최저순위"
excerpt: "[Level 1] 구현."

categories:
  - Algorithm
tags:
  - 구현
---
[문제](https://programmers.co.kr/learn/courses/30/lessons/77484)는 다음과 같다.

오늘은 프로그래머스 로또의 최고순위와 최저순위를 풀어보도록 하자. 0인 것을 카운팅하고 맞을 것을 카운팅해주어 따로 정리를 해주었다. 그 후 예외처리로 최고순위와 최저순위를 각각 answer벡터에 저장해주었다.

```c++
                                     [코드]
#include <string>
#include <vector>

using namespace std;

vector<int> solution(vector<int> lottos, vector<int> win_nums) {
    vector<int> answer;
    //0인 것들의 갯수
    int zero_count=0;
    //확정 맞춘 갯수
    int correct_count=0;
    for(int i=0;i<lottos.size();i++){
        if(lottos[i]==0){
            zero_count++;
            continue;
        }
        for(int j=0;j<6;j++){
            if(lottos[i] == win_nums[j]){
                correct_count++;
                break;
            }
        }
    }
    
    //예외처리(만일 아예 틀렸을 때)
    if(correct_count==0 && zero_count==0){
        answer.push_back(6);
    }
    else{
        answer.push_back(7-(correct_count+zero_count));
    }
    
    //예외처리(만일 0인 것은 있을 때)
    if(correct_count==0){
        answer.push_back(6);
    }
    else{
        answer.push_back(7-correct_count);
    }
    
    return answer;
}
```
