---
title:  "[C++]SW Expert Academy 수영장"
excerpt: "[D4] DFS or DP."

categories:
  - Algorithm
tags:
  - DFS
  - Dynamic Programming
---
[문제](https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AV5PpFQaAQMDFAUq)는 다음과 같다.

오늘은 SW Expert Academy 수영장 문제를 풀어보도록 하자. 삼성 기출문제인 감시문제와 비슷한 문제이다. dfs를 5개를 돌려보며 가능한 가짓수를 다 돌려보는 것이다.

DP로 푸는 방법이 있다고 한다. 다음에 DP공부를 할 때 DP로 다시 풀어봐야겠다.

```c++
                                     [코드]
#include <iostream>
using namespace std;
 
int year[13];
int price[4];
int answer;
 
void dfs(int month, int temp) {
    if (month > 12) {
        if (answer > temp) {
            answer = temp;
        }
        return;
    }
    if (year[month] == 0) {
        dfs(month + 1, temp);
    }
    dfs(month + 1, temp + year[month] * price[0]);
    dfs(month + 1, temp + price[1]);
    dfs(month + 3, temp + price[2]);
    dfs(month + 12, temp + price[3]);
}
 
int main() {
    ios::sync_with_stdio(false);
    cin.tie(0);
 
    int T, num = 0;
 
    cin >> T;
 
    while (T--) {
        answer = 987654321;
        for (int i = 0; i < 4; i++) {
            cin >> price[i];
        }
        for (int i = 1; i < 13; i++) {
            cin >> year[i];
        }
        dfs(1, 0);
        cout << '#' << ++num << ' ' << answer << '\n';
    }
}
```
