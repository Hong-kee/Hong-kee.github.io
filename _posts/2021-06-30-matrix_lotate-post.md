---
title:  "[C++]프로그래머스 행렬 테두리 회전하기"
excerpt: "[Level 2] 구현"

categories:
  - Algorithm
tags:
  - 구현
---
[문제](https://programmers.co.kr/learn/courses/30/lessons/77485#)는 다음과 같다.

오늘은 프로그래머스 행렬 테두리 회전하기를 풀어보도록 하자. 일반적인 회전이라하면 90도 시계 또는 반시계 회전이 주로 내는 문제이지만 위 문제는 한 칸씩 시계 방향으로 움직이는 문제였다. swap함수를 쓰거나 map[i][j + 1] = map[i][j] 의 형식으로 temp를 쓰면서 풀어도 된다.

나는 swap함수를 썼고, 일반적인 구현 문제이므로 주석을 확인하도록 합시다 :)

```c++
                                     [코드]
#include <iostream>
#include <string>
#include <vector>
#include <cmath>

using namespace std;

vector<int> answer;//정답
int map[101][101];//맵 설정

void Lotate_Map(vector<int>query){
    //시작 지점 to 끝 지점 설정
    int start_y = query[0];
    int start_x = query[1];
    int end_y = query[2];
    int end_x = query[3];
    int compare_num = map[start_y][start_x];//가장 작은 수 찾기위한 변수 선언
    
    //cout<<start_y<<' '<<start_x<<' '<<end_y<<' '<<end_x<<'\n';----값 입력 확인
    
    //1. 첫 번째 세로
    for(int i = start_y; i < end_y; i++){
        swap(map[i][start_x], map[i + 1][start_x]);
        compare_num = min(map[i][start_x], compare_num);
    }
    
    //2. 첫 번째 가로
    for(int i = start_x; i < end_x; i++){
        swap(map[end_y][i], map[end_y][i + 1]);
        compare_num = min(map[end_y][i], compare_num);
    }
    
    //3. 두 번째 세로
    for(int i = end_y; i > start_y; i--){
        swap(map[i][end_x], map[i - 1][end_x]);
        compare_num = min(map[i][end_x], compare_num);
    }
    
    //4. 두 번째 가로
    for(int i = end_x; i > start_x + 1; i--){
        swap(map[start_y][i], map[start_y][i - 1]);
        compare_num = min(map[start_y][i], compare_num);
    }
    answer.push_back(compare_num);
}

vector<int> solution(int rows, int columns, vector<vector<int>> queries) {
    int num = 1;
    
    for(int i = 1; i <= rows; i++){
        for(int j = 1; j <= columns; j++){
            map[i][j] = num; //맵의 값 설정
            num++;
        }
    }
    
    // for(int i = 1; i <= 6; i++){ -------입력 확인
    //     for(int j = 1; j <= 6; j++){
    //         cout<<map[i][j]<<' ';
    //     }
    //     cout<<'\n';
    // }
    
    for(int i = 0; i < queries.size(); i++){ //query수 만큼 실행
        Lotate_Map(queries[i]);
    }
    return answer;
}
```
