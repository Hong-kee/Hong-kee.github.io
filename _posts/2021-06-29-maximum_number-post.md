---
title:  "[C++]프로그래머스 수식 최대화"
excerpt: "[Level 2] 문자열 & DFS"

categories:
  - Algorithm
tags:
  - 문자열
  - DFS
---
[문제](https://programmers.co.kr/learn/courses/30/lessons/67257)는 다음과 같다.

오늘은 프로그래머스 수식 최대화를 풀어보도록 하자. 2020 카카오 인턴십 기출문제라고 한다. 후.. 문자열 파싱하는데 골치아팠다. 역시 C++의 숙명인가보다. 우선 연산자의 우선순위를 정해야한다. 따라서 DFS로 순열을 짜서 벡터에 넣어줘야 한다.

로직은 다음과 같다.

1. parsing_expression 벡터에 숫자와 문자를 string 형태로 파싱하여 저장한다.
2. OrderOperand함수를 통해 순열을 만들어 연산자 우선순위를 정해준다.
3. Calculation함수를 통해 우선순위를 따라 임시 변수 값에 저장하고 answer과 비교 후 절댓값이 더 크면 answer에 저장한다.

위 3단계 로직을 구현하면 풀 수 있는 문제였다. 로직은 간단한데 역시 문제는 parsing...

더 노력해서 C++ parsing Master가 되어야겠다.


```c++
                                     [코드]
#include <iostream>
#include <string>
#include <vector>
#include <cmath>

using namespace std;

char operand[3] = {'*', '+', '-'};//연산자 선언
bool visited[3];//방문처리
long long answer = 0;//정답
vector<char>operand_order;

void Calculation(long long compare_answer, vector<string> parsing_expression){//계산 돌리는 함수
    //for(int i = 0; i < 3; i++)cout<<operand_order[i]<<'\n';//출력
    long long temp_num;
    
    for(int i = 0; i < 3; i++){ //연산자 갯수 3개로 fix
        for(int j = 0; j < parsing_expression.size(); j++){//파싱 사이즈만큼 돌리기
            if(operand_order[i] == '*' && parsing_expression[j] == "*"){
                //cout<<' '<<i<<' '<<j<<'\n';---출력
                temp_num = stoll(parsing_expression[j - 1]) * stoll(parsing_expression[j + 1]);
                parsing_expression[j - 1] = to_string(temp_num);
                parsing_expression.erase(parsing_expression.begin() + j, parsing_expression.begin() + j + 2);
                j--;
                //for(int k = 0; k < parsing_expression.size(); k++)cout<<parsing_expression[k]<<' ';---출력
                //cout<<'\n';

            }
            if(operand_order[i] == '+'&& parsing_expression[j] == "+"){
                //cout<<' '<<i<<' '<<j<<'\n';---출력
                temp_num = stoll(parsing_expression[j - 1]) + stoll(parsing_expression[j + 1]);
                parsing_expression[j - 1] = to_string(temp_num);
                parsing_expression.erase(parsing_expression.begin() + j, parsing_expression.begin() + j + 2);
                j--;
                //for(int k = 0; k < parsing_expression.size(); k++)cout<<parsing_expression[k]<<' ';---출력
                //cout<<'\n';

            }
            if(operand_order[i] == '-' && parsing_expression[j] == "-"){
                //cout<<' '<<i<<' '<<j<<'\n';---출력
                temp_num = stoll(parsing_expression[j - 1]) - stoll(parsing_expression[j + 1]);
                parsing_expression[j - 1] = to_string(temp_num);
                parsing_expression.erase(parsing_expression.begin() + j, parsing_expression.begin() + j + 2);
                j--;
                //for(int k = 0; k < parsing_expression.size(); k++)cout<<parsing_expression[k]<<' ';---출력
                //cout<<'\n';
            }
        }
    }
    compare_answer = stoll(parsing_expression[0]);//string to long long
    compare_answer = abs(compare_answer);//convert to absolute number
    if(compare_answer > answer)answer = compare_answer;//compare to answer
}

void OrderOperand(int cnt, vector<string> parsing_expression){//조합짜고 계산으로 넘기는 함수
    if(cnt == 3){//연산자 선택이 3개가 이루어졌으면 ?
        Calculation(0, parsing_expression);
        return;
    }
    for(int i = 0; i < 3; i++){ //조합식
        if(visited[i])continue;
        operand_order.push_back(operand[i]);
        visited[i] = true;
        OrderOperand(cnt + 1, parsing_expression);
        operand_order.pop_back();
        visited[i] = false;
    }
}

long long solution(string expression) {
    string num_parse = "";//값 저장 임시 string
    vector<string>parsing_expression;//값과 연산자 저장
    
    for(int i = 0; i < expression.length(); i++){
        if(expression[i] == '*' || expression[i] == '+' || expression[i] == '-'){
            parsing_expression.push_back(num_parse);//값 저장
            string s = "";
            s += expression[i];
            parsing_expression.push_back(s);//연산자 저장
            num_parse = "";//값 초기화
        }
        else num_parse += expression[i];//값 잇기
    }
    parsing_expression.push_back(num_parse);//마지막 값 저장
    
    //for(int i = 0; i < parsing_expression.size(); i++){//파싱 출력값
    //   cout<<parsing_expression[i]<<' ';
    //}
    //cout<<'\n';
    
    OrderOperand(0, parsing_expression);
    return answer;
}
```
