---
title:  "[C++]프로그래머스 두 개 뽑아서 더하기"
excerpt: "[Level 1] 구현"

categories:
  - Algorithm
tags:
  - 구현
---
[문제](https://programmers.co.kr/learn/courses/30/lessons/68644)는 다음과 같다.

오늘은 프로그래머스 두 개 뽑아서 더하기를 풀어보도록 하자.

주석 참고 : )

```c++
                                     [코드]
#include <string>
#include <vector>
#include <algorithm>
using namespace std;

vector<int> solution(vector<int> numbers) {
    //정답
    vector<int> answer;
    //2개를 뽑아서 더하는 로직
    for(int first=0;first<numbers.size();first++){
        for(int second=first+1;second<numbers.size();second++){
            answer.push_back(numbers[first]+numbers[second]);
        }
    }
    //오름차순 정렬
    sort(answer.begin(), answer.end());
    //중복제거
    answer.erase(unique(answer.begin(),answer.end()),answer.end());
    return answer;
}
```
