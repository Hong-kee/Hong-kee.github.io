---
title:  "[C++]프로그래머스 삼각 달팽이"
excerpt: "[Level 2] 구현"

categories:
  - Algorithm
tags:
  - 구현
---
[문제](https://programmers.co.kr/learn/courses/30/lessons/68645)는 다음과 같다.

오늘은 프로그래머스 삼각 달팽이를 풀어보도록 하자. 우선 2차원 배열을 만들었다. 값이 할당되는 방향의 순환이 있다. (남, 동, 북서)를 계속 순환하면서 값이 매겨진다. 그리고 우리가 매겨야할 값의 총 카운트는 

입력 값 n을 기준으로 n * (n + 1) / 2번을 돌리면 된다. 왜냐하면 등차수열을 생각해보면 만일, n = 4면 1 + 2 + 3 + 4 = 10번을 할당하면 된다. 따라서 공차가 1인 등차수열의 합 공식을 쓰면 되고 할당 할 때 마다 1씩 빼주면 된다. 

그리고 방향전환 함수를 만들어 주고, 경계조건 함수인 Inbound함수를 설정하므로써 index를 움직여주었다. 자세한건 주석을 보면 알 수 있다 : ) 그리 어렵지 않다 !

```c++
                                     [코드]
#include <vector>

using namespace std;

//남, 동, 북서 방향으로 순환

int dir[3][2] = { {1, 0}, {0, 1}, {-1, -1} };//방향 설정
//맵 설정
int triangle[1001][1001];
int number = 1, direction = 0; //값, 방향

int ChangeDirection(int direction){
    if(direction == 0)return 1;
    else if(direction == 1) return 2;
    else return 0;
}

bool Inbound(int y, int x, int n){ //경계조건 함수
    return y >= 1 && y <= n && x >= 1 && x <= n;
}

vector<int> solution(int n) {
    vector<int> answer; //정답
    int total_count = n * (n + 1) / 2; //총 돌아야하는 횟수
    int y = 0, x = 1; //첫 좌표 설정
    
    while(total_count != 0){
        //좌표변환
        y += dir[direction][0];
        x += dir[direction][1];
        
        if(Inbound(y, x, n) && triangle[y][x] <= 0){ // 만일 경계 안이고, 값이 저장될 수 있는 곳이면 ?
            triangle[y][x] = number;//값 할당
            number++; // 값 증가
            total_count--;// total --
            continue;
        }
        //만일 아니라면 ? 좌표 되돌리고 방향 전환해주기
        y -= dir[direction][0];
        x -= dir[direction][1];
        direction = ChangeDirection(direction);
    }
    
    //정답처리
    for(int i = 1; i <= n; i++){
        for(int j = 1; j <= i; j++){
            answer.push_back(triangle[i][j]);
        }
    }
    return answer;
}
```
