---
layout: post
title: "Programmers 코딩 테스트 고득점 Kit_ [완전탐색] 카펫"
date: 2020-03-11
categories: Programmers BruteForce C++
---

- 문제 유형: 완전탐색_가능한 모든 상황을 조사하는 알고리즘
- 난이도: level_02 (약 3,433명 완료)
- 사용 언어: C++ <br/><br/>

## 1. 문제
### 1) 카펫   
Leo는 카펫을 사러 갔다가 아래 그림과 같이 중앙에는 빨간색으로 칠해져 있고 테두리 1줄은 갈색으로 칠해져 있는 격자 모양 카펫을 봤습니다.<br/>

<img src="https://grepp-programmers.s3.amazonaws.com/files/ybm/7c94563a35/2ff27ac9-97d0-43a9-9cf8-a344b8e7912e.png" title alt="image.png">

Leo는 집으로 돌아와서 아까 본 카펫의 빨간색과 갈색으로 색칠된 격자의 개수는 기억했지만, 전체 카펫의 크기는 기억하지 못했습니다. Leo가 본 카펫에서 <u>갈색 격자의 수 brown, 빨간색 격자의 수 red가 매개변수로 주어질 때</u> **카펫의 가로, 세로 크기를 순서대로 배열에 담아 return** 하도록 solution 함수를 작성해주세요.
<br/>

### 2) 제한사항   
- 갈색 격자의 수 brown은 8 이상 5,000 이하인 자연수입니다.
- 빨간색 격자의 수 red는 1 이상 2,000,000 이하인 자연수입니다.
- 카펫의 가로 길이는 세로 길이와 같거나, 세로 길이보다 깁니다.

### 3) 기본코드
```c++
#include <string>
#include <vector>

using namespace std;

vector<int> solution(int brown, int red) {
    vector<int> answer;
    return answer;
}
```
<br/><br/>

## 2. 알고리즘! 생각해보자
1) 문제로부터 생각해낼 수 있는 식 3가지
  - brown+red = 전체카펫 = width*high (단, width>=3, high>=3)
  - brown = 2(width+high-2)
  - red = (width-2)(high-2)

2) 첫번째 식으로부터 width와 high 가 무엇일지 추측해보기
  - 단, 2번째와 3번째 조건을 만족하는 width와 high일 것!
  - width 추측할 때 total/3부터 시작 (전체카펫 = width*high => width = 전체카펫/high(단, high>=3) = 전체카펫/3)

<br/><br/>

## 3. 해결코드
[C++]<br/>

```c++
#include <string>
#include <vector>

using namespace std;

vector<int> solution(int brown, int red) {
  vector<int> answer;

  //1.brown+red = 전체카펫 = width*high (단, high>=3)
  int total = brown+red;

  //2.첫번째 식으로부터 width와 high 가 무엇일지 추측
  for(int i=total/3; i>2; i--){
      if(total%i == 0 && total/i >= 3){
          if(red == (i-2)*((total/i)-2) && brown/2 == i+(total/i)-2){
              //width 설정
              answer.push_back(i);
              break;
          }            
      }
  }    

  //high 설정
  answer.push_back(total/answer[0]);

  return answer;
}
```
<br/><br/>

## 4. 문제해결능력 UP! 되짚어보기
- 문제를 통해 같은 식을 도출했지만, 다른 방법을 통해 더 간단히 해결가능
  <br/>brown = 2(width+high-2) => brown/2 + 2 = width+high => length = brown/2 + 2
<br/><br/>

## 5. References
1) 공식 C++ References (<https://modoocode.com/241>)
<br/><br/>
