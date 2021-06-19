---
title:  "[C++]프로그래머스 크레인 인형뽑기 게임"
excerpt: "[Level 1] 구현."

categories:
  - Algorithm
tags:
  - 구현
---
[문제](https://programmers.co.kr/learn/courses/30/lessons/64061)는 다음과 같다.

오늘은 프로그래머스 크레인 인형뽑기 게임를 풀어보도록 하자. 일반적인 구현문제로 카카오 문제치곤 까다롭지도 않은 구현문제였다. 하라는대로 하면 되는(?) 문제였다. :) 주석을 잘 보고 이해해보자! 

```c++
                                     [코드]
#include <string>
#include <vector>

using namespace std;

int solution(vector<vector<int>> board, vector<int> moves) {
    //정답
    int answer = 0;
    //바구니 벡터 생성
    vector<int> basket;
    
    //moves의 번수 만큼
    for(int i=0;i<moves.size();i++){
        //move index설정
        int moves_idx = moves[i] - 1;
        for(int j=0;j<board.size();j++){
            //만일 비어있지 않다면
            if(board[j][moves_idx] != 0){
                //바구니에 담고 보드 0처리
                basket.push_back(board[j][moves_idx]);
                board[j][moves_idx] = 0;
                //만일 바구니 안에 같은게 2개라면
                if(basket.size() > 1 && (basket.back() == basket[basket.size()-2])){
                    answer += 2;
                    basket.pop_back();
                    basket.pop_back();
                }
                break;
            }
        }
    }
    
    return answer;
}
```
