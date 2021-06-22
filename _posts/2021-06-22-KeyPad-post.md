---
title:  "[C++]프로그래머스 키패드 누르기"
excerpt: "[Level 1] 구현."

categories:
  - Algorithm
tags:
  - 구현
---
[문제](https://programmers.co.kr/learn/courses/30/lessons/67256)는 다음과 같다.

오늘은 프로그래머스 키패드 누르기를 풀어보도록 하자. 단순 구현문제이다. 함수를 잘 나누어주고 만일 2,5,8,0이라면 거리와 hand를 따져서 어느 손으로 누를지 선택하면 되겠다. : )

```c++
                                     [코드]
#include <string>
#include <vector>
#include <cmath>

using namespace std;

//1,4,7은 Left, 3,6,9는 Right
//2,5,8,0은 거리를 우선 생각해보고 가까운 hand로-> 만일 거리가 가깝다면 hand고려

//키패드 설정(*은 10, #은 11)
vector<vector<int>>key_pad(4,vector<int>(3,0));
//처음 키패드 시작부분 설정
int left_y=3, left_x=0,right_y=3,right_x=2;
//정답(답은 append로 하고 대문자로)
string answer = "";

//왼쪽 세팅
void LeftSetting(int number){
    for(int i=0;i<key_pad.size();i++){
        for(int j=0;j<key_pad[i].size();j++){
            if(number == key_pad[i][j]){
                left_y = i;
                left_x = j;
                answer += 'L';
                return;
            }
        }
    }
}

//오른쪽 세팅
void RightSetting(int number){
    for(int i=0;i<key_pad.size();i++){
        for(int j=0;j<key_pad[i].size();j++){
            if(number == key_pad[i][j]){
                right_y = i;
                right_x = j;
                answer += 'R';
                return;
            }
        }
    }
}

//가운데 세팅
void MiddleSetting(int number, string hand){
    for(int i=0;i<key_pad.size();i++){
        for(int j=0;j<key_pad[i].size();j++){
            if(number == key_pad[i][j]){
                //오른손이 더 가깝다
                if(abs(right_y-i)+abs(right_x-j) < abs(left_y-i)+abs(left_x-j)){
                    right_y=i;
                    right_x=j;
                    answer+='R';
                }
                //왼손이 더 가깝다
                else if(abs(right_y-i)+abs(right_x-j) > abs(left_y-i)+abs(left_x-j)){
                    left_y=i;
                    left_x=j;
                    answer+='L';
                }
                //같다
                else{
                    if(hand == "right"){
                        right_y=i;
                        right_x=j;
                        answer+='R';
                    }
                    else{
                        left_y=i;
                        left_x=j;
                        answer+='L';
                    }
                }
                return;
            }
        }
    }
}
//키패드 
void KeyPadSetting(){
    key_pad[0][0]=1;key_pad[0][1]=2;key_pad[0][2]=3;
    key_pad[1][0]=4;key_pad[1][1]=5;key_pad[1][2]=6;
    key_pad[2][0]=7;key_pad[2][1]=8;key_pad[2][2]=9;
    key_pad[3][0]=10;key_pad[3][1]=0;key_pad[3][2]=11;
}

string solution(vector<int> numbers, string hand) {
    //키패드 세팅
    KeyPadSetting();
    //number size만큼 for문 돌기
    for(int i=0;i<numbers.size();i++){
        //Left설정
        if(numbers[i] == 1 || numbers[i] == 4 || numbers[i] == 7){
            LeftSetting(numbers[i]);
        }
        //Right설정
        else if(numbers[i] == 3 ||numbers[i] == 6 ||numbers[i] == 9){
            RightSetting(numbers[i]);
        }
        //중간부분설정
        else{
            MiddleSetting(numbers[i], hand);
        }
    }
    return answer;
}
```
