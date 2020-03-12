---
layout: post
title: "Programmers 코딩 테스트 고득점 Kit_ [완전탐색] 탑"
date: 2020-03-11
categories: Programmers Stack-Queue C++
---

- 문제 유형: Stack/Queue
- 난이도: level_02 (약 7,959명 완료)
- 사용 언어: C++ <br/><br/>

## 1. 문제
### 1) 탑   
수평 직선에 탑 N대를 세웠습니다. 모든 탑의 꼭대기에는 신호를 송/수신하는 장치를 설치했습니다. 발사한 신호는 신호를 보낸 탑보다 높은 탑에서만 수신합니다. 또한, 한 번 수신된 신호는 다른 탑으로 송신되지 않습니다.<br/>

예를 들어 높이가 6, 9, 5, 7, 4인 다섯 탑이 왼쪽으로 동시에 레이저 신호를 발사합니다. 그러면, 탑은 다음과 같이 신호를 주고받습니다. 높이가 4인 다섯 번째 탑에서 발사한 신호는 높이가 7인 네 번째 탑이 수신하고, 높이가 7인 네 번째 탑의 신호는 높이가 9인 두 번째 탑이, 높이가 5인 세 번째 탑의 신호도 높이가 9인 두 번째 탑이 수신합니다. 높이가 9인 두 번째 탑과 높이가 6인 첫 번째 탑이 보낸 레이저 신호는 어떤 탑에서도 수신할 수 없습니다.
<br/>

<table border='1' bordercolor='black' width ='40%'>
  <tr style="background-color:#e3e3e3">
    <th>송신탑(높이)</th>
    <th>수신탑(높이)</th>
  </tr>
  <tr>
    <td align ="center">5(4)</td>
    <td align ="center">4(7)</td>
  </tr>
  <tr>
    <td align ="center">4(7)</td>
    <td align ="center">2(9)</td>
  </tr>
  <tr>
    <td align ="center">3(5)</td>
    <td align ="center">2(9)</td>
  </tr>
  <tr>
    <td align ="center">2(9)</td>
    <td align ="center">-</td>
  </tr>
  <tr>
    <td align ="center">1(6)</td>
    <td align ="center">-</td>
  </tr>
</table>

맨 왼쪽부터 순서대로 탑의 높이를 담은 배열 heights가 매개변수로 주어질 때 각 탑이 쏜 신호를 어느 탑에서 받았는지 기록한 배열을 return 하도록 solution 함수를 작성해주세요.
<br/>

### 2) 제한사항   
- heights는 길이 2 이상 100 이하인 정수 배열입니다.
- 모든 탑의 높이는 1 이상 100 이하입니다.
- 신호를 수신하는 탑이 없으면 0으로 표시합니다.

### 3) 기본코드
```c++
#include <string>
#include <vector>

using namespace std;

vector<int> solution(vector<int> heights) {
    vector<int> answer;
    return answer;
}
```
<br/><br/>

## 2. 알고리즘! 생각해보자
1) 가장 뒤에 있는 탑부터 송신시작
  - 자신보다 높은 탑이 있다면, answer에 추가 & 송신 stop
  - 그렇지 않다면, continue

2) 송신을 마쳤는데, 자기자신이라면(=송신자가 없다면...) "-1"(3번째 단계에서 0으로 저장하기 위해) 저장<br/>
3) index로 계산된 answer를 송신탑 순서로 맞추기 위해 전체 +1
<br/><br/>

## 3. 해결코드
[C++]<br/>

```c++
#include <string>
#include <vector>

using namespace std;

vector<int> solution(vector<int> heights) {
    vector<int> answer;

    //1.가장 뒤에 있는 탑부터 송신시작
    answer.resize(heights.size());
    for(int i=heights.size()-1; i>=0; i--){
        answer[i] = i;
        for(int j=i-1; j>=0; j--){
          //1-1.자신보다 높은 탑이 있다면, answer에 추가 & 송신 stop
            if(heights[answer[i]] < heights[j]){
                answer[i] = j;
                break;
            }
        }
        //2.송신을 마쳤는데, 자기자신이라면(=송신자가 없다면...) -1(3번째 단계에서 0으로 저장하기 위해) 저장
        if(answer[i] == i)
            answer[i] = -1;
    }
    //3.index로 계산된 answer를 송신탑 순서로 맞추기 위해 전체 +1
    for(int i=0; i<answer.size(); i++){
        answer[i]++;
    }

    return answer;
}
```
<br/><br/>

## 4. 문제해결능력 UP! 되짚어보기
- 뒤에서부터 계산하는 방법말고, 앞에서부터 계산하는 방법 생각해보기(index 잘 계산하기)
- 스택에서 push하는 것이 vector 자료형에서는 push_back의 개념이 활용된 것

<br/><br/>

## 5. References
1) 공식 C++ References (<https://modoocode.com/241>)
<br/><br/>
