---
layout: post
title: "Programmers 코딩 테스트 고득점 Kit_ [스택-큐] 주식가격"
date: 2020-03-16
categories: Programmers Stack-Queue C++
---

- 문제 유형: 스택-큐_LIFO-FIFO 자료형
- 난이도: level_02 (약 4,908명 완료)
- 사용 언어: C++ <br/><br/>

## 1. 문제
### 1) 주식가격
초 단위로 기록된 주식가격이 담긴 배열 prices가 매개변수로 주어질 때, 가격이 떨어지지 않은 기간은 몇 초인지를 return 하도록 solution 함수를 완성하세요.
<br/>

### 2) 제한사항   
- prices의 각 가격은 1 이상 10,000 이하인 자연수입니다.
- prices의 길이는 2 이상 100,000 이하입니다.

### 3) 기본코드
```c++
#include <string>
#include <vector>

using namespace std;

vector<int> solution(vector<int> prices) {
    vector<int> answer;
    return answer;
}
```
<br/><br/>

## 2. 알고리즘! 생각해보자
1) 문제 제대로 이해하기: <u>"주식 가격이 떨어지는 시점"</u>에서 시간 계산
<br/><br/>

## 3. 해결코드
[C++]<br/>

```c++
#include <string>
#include <vector>

using namespace std;

vector<int> solution(vector<int> prices) {
    vector<int> answer(prices.size(), 0);

    for(int i=0; i<prices.size()-1; i++){
        for(int j=i+1; j<prices.size(); j++){
            (*(answer.begin()+i))++;
            if(prices[i] > prices[j]) break;
        }
    }

    return answer;
}
```
<br/><br/>

## 4. 문제해결능력 UP! 되짚어보기
- 처음에 문제를 제대로 이해하지 못해서 시간을 많이 할애함, 문제에서 "주식가격이 떨어지지 않은 기간은 몇 초인지를 return"하라고 하였는데, 이 말은 즉, 주식가격이 떨어지는 시점에서 기간을 계산하면 되는 것이었음

<br/><br/>

## 5. References
1) 공식 C++ References (<https://modoocode.com/241>)
<br/><br/>
