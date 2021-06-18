---
title:  "[C++]프로그래머스 소수 만들기"
excerpt: "[Level 1] DFS."

categories:
  - Algorithm
tags:
  - DFS
---
[문제](https://programmers.co.kr/learn/courses/30/lessons/12977)는 다음과 같다. DFS를 이용하여 중복 없이 벡터원소 중 3개를 뽑아 더하고 소수인지 판별하는 문제였다. 만일 입력 갯수가 컸으면 에라토스테네스의 체를 썼을 것이다. 하지만 입력 데이터의 갯수가 크지 않아서 그냥 함수로 만들어서 했다.

그래도 약간의 최적화를 위해 소수판별을 할 때 total까지가 아닌 total/2 까지 나눠주는 센스(?)로 약간의 시간을 줄일 수가 있다 ! :)

```c++
                                     [코드]
#include <vector>
using namespace std;

int answer=0;

//소수 판별 함수
bool isPrime(int total){
    for(int i=2;i<total/2;i++){
        //만일 i로 나뉘어진다면 소수가 아니다.
        if(total % i == 0){
            return false;
        }
    }
    //i로 안 나뉘었을 때 true반환
    return true;
}

void pick_num(vector<int> &nums, int idx, int cnt, int total){
    //만약 3개를 뽑으면
    if(cnt == 3){
        //만약 총합이 소수면
        if(isPrime(total)){
            //갯수 +1 카운트
            answer++;
        }
        return;
    }
    //중복없는 조합 로직(dfs)
    for(int i=idx;i<nums.size();i++){
        pick_num(nums, i+1, cnt+1, total + nums[i]);
    }
}

int solution(vector<int> nums) {
    //dfs로 조합 만들기
    pick_num(nums, 0, 0, 0);
    return answer;
}
```
