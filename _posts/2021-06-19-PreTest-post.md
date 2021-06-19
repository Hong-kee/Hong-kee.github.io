---
title:  "[C++]프로그래머스 모의고사"
excerpt: "[Level 1] 구현."

categories:
  - Algorithm
tags:
  - 구현
---
[문제](https://programmers.co.kr/learn/courses/30/lessons/42840)는 다음과 같다.

오늘은 프로그래머스 모의고사를 풀어보도록 하자. 1번, 2번, 3번 수포자의 찍는 패턴을 각 벡터에 저장해둔 후 Modulation연산을 해주어 각 점수를 카운팅해주었다. 그 후에 세 사람의 점수를 비교하여 정렬을 구현하면 끝!

```c++
                                     [코드]
#include <string>
#include <vector>

using namespace std;

//1 : 1 2 3 4 5 --> 5개
//2 : 2 1 2 3 2 4 2 5 --> 8개
//3 : 3 3 1 1 2 2 4 4 5 5 --> 10개

vector<int> solution(vector<int> answers) {
    //정답 벡터
    vector<int> answer;
    //각 수포자들의 패턴 저장
    vector<int> first({1,2,3,4,5}), second({2,1,2,3,2,4,2,5}), third({3,3,1,1,2,2,4,4,5,5});
    //점수 저장 변수 설정
    int first_score=0;
    int second_score=0;
    int third_score=0;
    //각 점수 배점
    for(int i=0;i<answers.size();i++){
        if(answers[i]==first[i%5])first_score++;
        if(answers[i]==second[i%8])second_score++;
        if(answers[i]==third[i%10])third_score++;
    }
    //7 7 6 --> 1 2 3
    answer.push_back(1);
    //두 번째 수가 더 크다면
    if(first_score < second_score){
        answer.pop_back();
        answer.push_back(2);
    }//같다면
    else if(first_score == second_score){
        answer.push_back(2);
    }
    //만일 1,2번이 동점인데 3번이 제일 잘했음
    if(answer.size() == 2){
        if(second_score < third_score){
            answer.clear();
            answer.push_back(3);
        }
        else if(second_score == third_score){
            answer.push_back(3);
        }
    }
    else{
        //1번일 때
        if(answer.back() == 1){
            if(first_score < third_score){
                answer.pop_back();
                answer.push_back(3);
            }
            else if(first_score == third_score){
                answer.push_back(3);
            }
        }
        //2번일 때
        else{
            if(second_score < third_score){
                answer.pop_back();
                answer.push_back(3);
            }
            else if(second_score == third_score){
                answer.push_back(3);
            }
        }
    }
    
    return answer;
}
```
