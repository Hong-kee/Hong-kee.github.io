---
title:  "[C++]프로그래머스 튜플"
excerpt: "[Level 2] 문자열 & Sort"

categories:
  - Algorithm
tags:
  - 문자열
  - Sort
---
[문제](https://programmers.co.kr/learn/courses/30/lessons/64065)는 다음과 같다.

오늘은 프로그래머스 튜플을 풀어보도록 하자. pair vector를 이용, 정렬을 쓰는 문제이다. 나는 카운팅소트를 이용했다. pair 벡터에 (cnt, idx)를 넣어주고, 튜플 값을 string to int 처리하여 벡터의 대응 인덱스에 카운트해주었다. 

그 후 first를 기준으로 내림차순 정렬을 하여 인덱스를 뽑아냈다.

```c++
                                     [코드]
#include <iostream>
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

vector<int> solution(string s) {
    vector<int> answer;//정답
    vector<pair<int, int>> cnt_idx;//카운팅소트하기 위한 벡터
    string number = "";//임시 string class 
    
    for(int i = 1; i <= 100001; i++) cnt_idx.push_back(make_pair(0, i - 1));// (cnt, idx)의 원소 삽입
    
    for(int i = 1; i < s.length() - 1; i++){
        if(s[i] == '{' || (s[i] == ',' && s[i-1] == '}')) continue; //만일 { ,이면 무관심
        else if(s[i] == '}' || (s[i] == ',' && s[i-1] != '}')) { // 만일 } 면 숫자 끝
            int num = stoi(number);//string to int
            cnt_idx[num].first++;//카운팅
            number = "";//초기화
        }
        else number += s[i];// 만일 숫자면 이어 붙이기
    }
   
    sort(cnt_idx.begin(), cnt_idx.end(),greater<>());
   
    //출력 
    // for(int i = 0; i < 6; i++){
    //     cout<<cnt_idx[i].first<<' '<<cnt_idx[i].second<<' ';
    //     cout<<'\n';
    // }
    
    for(int i = 0; i < cnt_idx.size(); i++){
        if(cnt_idx[i].first == 0)break;
        else answer.push_back(cnt_idx[i].second);
    }
    return answer;
}
```
