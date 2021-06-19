---
title:  "[C++]프로그래머스 폰켓몬"
excerpt: "[Level 1] Sort."

categories:
  - Algorithm
tags:
  - Sort
---
[문제](https://programmers.co.kr/learn/courses/30/lessons/1845)는 다음과 같다.

```c++
                                     [코드]
#include <vector>
#include <algorithm>
using namespace std;

int solution(vector<int> nums){
    //정답 갯수
    int answer = 0;
    //총 뽑을 수 있는 가짓 수
    int pick_count = nums.size() / 2;
    //정렬 후 중복원소 제거
    sort(nums.begin(), nums.end());
    nums.erase(unique(nums.begin(), nums.end()),nums.end());

    //만일 뽑을 가짓 수가 중복 제거된 사이즈보다 크거나 같다면
    if(pick_count >= nums.size()){
        answer = nums.size();
    }
    else{
        answer = pick_count;
    }
    
    return answer;
}
```
