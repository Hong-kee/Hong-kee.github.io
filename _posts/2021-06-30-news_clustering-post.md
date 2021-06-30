---
title:  "[C++]프로그래머스 1차 뉴스 클러스터링"
excerpt: "[Level 2] 문자열 & Math"

categories:
  - Algorithm
tags:
  - 문자열
  - Math
---
[문제](https://programmers.co.kr/learn/courses/30/lessons/17677)는 다음과 같다.

오늘은 프로그래머스 1차 뉴스 클러스터링를 풀어보도록 하자. 문자열을 처리하는 문제이다. 2개씩 문자열 파싱을 하면서 소문자는 대문자로 변환하고 영어가 아닌 것은 빼서 각 벡터에 저장한다. 그리고 같은 문장이 나오면 check배열을 통해 중복을 처리해준다.

그 후 교집합 갯수는 true인 것이 있으면 +1해주고 합집합 갯수는 false가 있으면 +1씩 해준 후, 마지막에 union_cnt에 intersection_cnt를 더해주면 된다. 주의할 것이 있다. 마지막에 나누는 인자. 즉, union_cnt가 0이면 0으로 나누는 것이기 때문에 answer = 65536으로 처리해준다.

자세한 과정은 주석을 보시면 되겠따 : )

```c++
                                     [코드]
#include <iostream>
#include <string>
#include <vector>

using namespace std;

bool check_str1[1002];//1번에 대한 중복체크
bool check_str2[1002];//2번에 대한 중복체크

int solution(string str1, string str2) {
    int answer = 0, intersection_cnt = 0, union_cnt = 0;//정답, 교집합 갯수, 합집합 갯수
    
    vector<string> str1_set, str2_set; //각 부분집합 저장공간
    
    //str1에 대해 자르기
    for(int i = 0; i < str1.length(); i++){
        string sub_str1 = str1.substr(i, 2); //2글자씩

        for(int j = 0; j < 2; j++){
            if(sub_str1[j] >= 97 && sub_str1[j] <= 122) sub_str1[j] -= 32;//만일 소문자면 대문자로 바꿔서 넣기
            else if(sub_str1[j] >= 65 && sub_str1[j] <= 90) continue; //대문자면 통과
            else{
                sub_str1 = "";
                break;
            }
        }
        if(sub_str1.length() != 0) str1_set.push_back(sub_str1);//다 통과면 집어넣기
    }
     
    //str2에 대해 자르기
    for(int i = 0; i < str2.length(); i++){
        string sub_str2 = str2.substr(i, 2); //2글자씩

        for(int j = 0; j < 2; j++){
            if(sub_str2[j] >= 97 && sub_str2[j] <= 122) sub_str2[j] -= 32;//만일 소문자면 대문자로 바꿔서 넣기
            else if(sub_str2[j] >= 65 && sub_str2[j] <= 90) continue; //대문자면 통과
            else{
                sub_str2 = "";
                break;
            }
        }
        if(sub_str2.length() != 0) str2_set.push_back(sub_str2);//다 통과면 집어넣기
    }
    
    for(int i = 0; i < str1_set.size(); i++){//중복처리
        for(int j = 0; j < str2_set.size(); j++){
            if(str1_set[i] == str2_set[j] && !check_str2[j]){ // 같고 중복 아니라면 ?
                check_str1[i] = true;
                check_str2[j] = true;
                break;
            }
        }
    }
    
    for(int i = 0; i < str1_set.size(); i++){//겹치는거 세기(합집합)
        if(!check_str1[i]) union_cnt++;
    }
    for(int i = 0; i < str2_set.size(); i++){//겹치는거 세기(합집합)
        if(!check_str2[i]) union_cnt++;
    }
    for(int i = 0; i < str1_set.size(); i++){//겹치는거 세기(교집합)
        if(check_str1[i]) intersection_cnt++;
    }

    /*
    출력
    */
    // for(int i = 0; i < str1_set.size(); i++){
    //     cout<<str1_set[i]<<' ';
    // }
    // cout<<'\n';
    // for(int i = 0; i < str2_set.size(); i++){
    //     cout<<str2_set[i]<<' ';
    // }
    //cout<<'\n';
    
    union_cnt += intersection_cnt;
    
    //cout<<intersection_cnt<<' '<<union_cnt<<'\n';

    if(union_cnt == 0) answer = 65536;
    else answer = 65536 * intersection_cnt / union_cnt;
    return answer;
}
```
