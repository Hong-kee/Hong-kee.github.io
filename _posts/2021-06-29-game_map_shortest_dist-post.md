---
title:  "[C++]프로그래머스 게임 맵 최단거리"
excerpt: "[Level 2] BFS"

categories:
  - Algorithm
tags:
  - BFS
---
[문제](https://programmers.co.kr/learn/courses/30/lessons/1844)는 다음과 같다.

오늘은 프로그래머스 게임 맵 최단거리를 풀어보도록 하자. 전형적인 BFS문제이다. 최단거리를 탐색하는 문제는 BFS가 효과적이고 데이터의 크기도 100이하라 적합하다. 주석을 참고하자! : )

```c++
                                     [코드]
#include <vector>
#include <queue>
using namespace std;

bool visited[101][101];//maps의 방문처리 배열
int dir[4][2] = {{-1, 0}, {0, 1}, {1, 0}, {0, -1}};//4방향 설정 (북, 동, 남, 서)
int map_y, map_x, answer = -1;//맵 크기와 정답 변수 선언

struct pos{ //queue 안에 위치를 넣기위한 구조체 선언
    int y;
    int x;
    int cnt;
};

queue<pos>Q;//BFS를 위한 queue설정

bool Inbound(int y, int x){//경계범위 체크함수
    return y >= 0 && y <= map_y && x >= 0 && x <= map_x;
}

void BFS(int y, int x, vector<vector<int>>maps){//최단거리 탐색 BFS
    Q.push({0,0,1});//초깃값 설정
    visited[0][0] = true;//방문처리
    
    while(!Q.empty()){//큐가 안 비었다면 ?
        int y = Q.front().y;
        int x = Q.front().x;
        int cnt = Q.front().cnt;
        Q.pop();
        
        if(y == map_y && x == map_x){
            answer = cnt;//만일 도달할 수 있다면 ? answer 갱신
            break;
        }
        
        for(int i = 0; i < 4; i++){// 4방향 확인
            int m_y = y + dir[i][0];
            int m_x = x + dir[i][1];
            
            if(Inbound(m_y, m_x)){//경계 안에 있고
                if(maps[m_y][m_x] == 1 && !visited[m_y][m_x]){//갈 수 있는 곳이라면
                    Q.push({m_y, m_x, cnt + 1});//이동한 곳, 카운트 + 1을 큐에 넣기
                    visited[m_y][m_x] = true;//방문처리
                }
            }
        }
    }
}

int solution(vector<vector<int>> maps){
    map_y = maps.size() - 1;//맵 y크기
    map_x = maps[0].size() - 1;//맵 x크기
    BFS(0, 0, maps);
    return answer;
}
```
