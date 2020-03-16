---
layout: post
title: "Programmers 코딩 테스트 고득점 Kit_ [스택-큐] 기능개발"
date: 2020-03-14
categories: Programmers Stack-Queue C++
---

- 문제 유형: 스택-큐_LIFO-FIFO 자료형
- 난이도: level_02 (약 6,333명 완료)
- 사용 언어: C++ <br/><br/>

## 1. 문제
### 1) 기능개발
프로그래머스 팀에서는 기능 개선 작업을 수행 중입니다. 각 기능은 진도가 100%일 때 서비스에 반영할 수 있습니다. 또, 각 기능의 개발속도는 모두 다르기 때문에 뒤에 있는 기능이 앞에 있는 기능보다 먼저 개발될 수 있고, 이때 뒤에 있는 기능은 앞에 있는 기능이 배포될 때 함께 배포됩니다.<br/>

먼저 배포되어야 하는 순서대로 작업의 진도가 적힌 정수 배열 progresses와 각 작업의 개발 속도가 적힌 정수 배열 speeds가 주어질 때 각 배포마다 몇 개의 기능이 배포되는지를 return 하도록 solution 함수를 완성하세요.
<br/>

### 2) 제한사항   
- 작업의 개수(progresses, speeds배열의 길이)는 100개 이하입니다.
- 작업 진도는 100 미만의 자연수입니다.
- 작업 속도는 100 이하의 자연수입니다.
- 배포는 하루에 한 번만 할 수 있으며, 하루의 끝에 이루어진다고 가정합니다. 예를 들어 진도율이 95%인 작업의 개발 속도가 하루에 4%라면 배포는 2일 뒤에 이루어집니다.

### 3) 기본코드
```c++
#include <string>
#include <vector>

using namespace std;

vector<int> solution(vector<int> progresses, vector<int> speeds) {
    vector<int> answer;
    return answer;
}
```
<br/><br/>

## 2. 알고리즘! 생각해보자
1) 각 기능별로 몇 일 걸리는지 계산<br/>
2) 각 배포일 당 몇 개 기능이 출시될 수 있는지 계산
<br/><br/>

## 3. 해결코드
[C++]<br/>

```c++
#include <string>
#include <vector>

using namespace std;

vector<int> solution(vector<int> progresses, vector<int> speeds) {
    vector<int> answer;

    vector<int> dev_days;
    int temp;

    //1. 각 기능별로 몇 일 걸리는지 계산
    for(int i=0; i<progresses.size(); i++){
        temp = (100-progresses[i])/speeds[i];
        if((100-progresses[i])%speeds[i] == 0)
            dev_days.push_back(temp);
        else
            dev_days.push_back(temp+1);
    }

    //2.각 배포일 당 몇 개 기능이 출시될 수 있는지 계산
    int idx = 0;
    temp = dev_days[0];
    answer.push_back(1);
    for(int i=1; i<progresses.size(); i++){
        if(temp >= dev_days[i]){
            answer[idx]++;
        }
        else{
            temp = dev_days[i];
            answer.push_back(1);
            idx++;
        }
    }

    return answer;
}
```
<br/><br/>

## 4. 문제해결능력 UP! 되짚어보기
- vector에서 front()와 back() 적극사용 => 큐 개념 명확히 명시 가능

<br/><br/>

## 5. References
1) 공식 C++ References (<https://modoocode.com/241>)
<br/><br/>
