---
title:  "[C++]프로그래머스 가장 큰 수"
excerpt: "[Level 2] Sort & 문자열"

categories:
  - Algorithm
tags:
  - Sort
  - 문자열
---
[문제](https://programmers.co.kr/learn/courses/30/lessons/42746)는 다음과 같다.

오늘은 프로그래머스 가장 큰 수를 풀어보도록 하자. 우선 정답이 길 수 있으므로 문자열 처리를 해주어야 한다. 그 후 직접 비교함수를 만들어 정렬해준다. 예를 들어 6, 10, 2가 문자열 형태로 각각 저장되어있다고 하자.

그렇다면 처음엔 610, 106을 비교하게 되고 610이 크므로 가만히 둔다. 그 후 102와 210을 비교하고 210이 더 크므로 교환해준다. 그 후 62, 26을 비교하면 62가 더 크므로 가만히 둔다.

따라서 6, 2, 10으로 정렬이 되고 6210이라는 답이 나온다.

```c++
                                     [코드]
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

bool Compare(string s1, string s2){
    if(s1 + s2 <= s2 + s1) return false; // 만일 문자열을 이어붙인 것이 뒤에 것이 더 크면 교환
    return true;
}

string solution(vector<int> numbers) {
    string answer = "";//정답
    vector<string> store_number;//int to string 저장소
    
    for(int i = 0; i < numbers.size(); i++){ // int to string
        store_number.push_back(to_string(numbers[i]));
    }
    sort(store_number.begin(), store_number.end(),Compare);//비교함수 Compare을 기준으로 정렬
    
    for(int i = 0; i < store_number.size(); i++) answer += store_number[i];
    
    if(answer[0] == '0') answer= "0";// 만일 앞이 0으로 시작하면 답은 0
    
    return answer;
}
```
