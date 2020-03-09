---
layout: post
title: "Programmers 코딩 테스트 고득점 Kit_ [완전탐색] 모의고사"
date: 2020-03-09
categories: Programmers Hash C++
---

- 문제 유형: 완전탐색_가능한 모든 상황을 조사하는 알고리즘
- 난이도: level_01 (약 9,729명 완료)
- 사용 언어: C++ <br/><br/>

## 1. 문제
### 1) 모의고사   
수포자는 수학을 포기한 사람의 준말입니다. 수포자 삼인방은 모의고사에 수학 문제를 전부 찍으려 합니다. 수포자는 1번 문제부터 마지막 문제까지 다음과 같이 찍습니다.<br/>

1번 수포자가 찍는 방식: 1, 2, 3, 4, 5, 1, 2, 3, 4, 5, ...<br/>
2번 수포자가 찍는 방식: 2, 1, 2, 3, 2, 4, 2, 5, 2, 1, 2, 3, 2, 4, 2, 5, ...<br/>
3번 수포자가 찍는 방식: 3, 3, 1, 1, 2, 2, 4, 4, 5, 5, 3, 3, 1, 1, 2, 2, 4, 4, 5, 5, ...<br/>

1번 문제부터 마지막 문제까지의 정답이 순서대로 들은 배열 answers가 주어졌을 때, 가장 많은 문제를 맞힌 사람이 누구인지 배열에 담아 return 하도록 solution 함수를 작성해주세요.
<br/>

### 2) 제한사항   
- 시험은 최대 10,000 문제로 구성되어있습니다.
- 문제의 정답은 1, 2, 3, 4, 5중 하나입니다.
- 가장 높은 점수를 받은 사람이 여럿일 경우, return하는 값을 오름차순 정렬해주세요.

### 3) 기본코드
```c++
#include <string>
#include <vector>

using namespace std;

vector<int> solution(vector<int> answers) {
    vector<int> answer;
    return answer;
}
```
<br/>

## 2. 알고리즘! 생각해보자
1) 수포자별로 답안 작성 규칙 찾기
- 수포자1: 12345 반복
- 수포자2: 21232425 반복
- 수포자3: 3311224455 반복

2) 수포자별로 맞은 개수 count<br/>
3) 가장 점수 높은 수포자를 asnwer에 추가(동점인 경우 모두)하고 return
<br/><br/>

## 3. 해결코드
[C++]<br/>

```c++
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

vector<int> solution(vector<int> answers) {
    vector<int> answer;
    vector<int> answer_temp;

    int divider;
    int remainder;
    int cnt;
    int temp;

    // 1.수포자별 벡터 생성 및 초기화
    vector<int> spj1;
    vector<int> spj1_temp;
    vector<int> spj1_temp{1,2,3,4,5};
    vector<int> spj2;
    vector<int> spj2_temp{2,1,2,3,2,4,2,5};
    vector<int> spj3;
    vector<int> spj3_temp{3,3,1,1,2,2,4,4,5,5};

    // 2.수포자별 맞은개수 count
    // 2-1.spj1(수포자1)
    cnt = 0;
    temp = 0;
    for(int i =0;i<answers.size(); i++, cnt++){
        if(i%5 == 0) cnt = 0;
        if(answers[i] == spj1_temp[cnt]) temp = temp+1;
    }
    answer_temp.push_back(temp);

    // 2-1.spj2(수포자2)
    cnt = 0;
    temp = 0;
    for(int i =0;i<answers.size(); i++, cnt++){
        if(i%8 == 0) cnt = 0;
        if(answers[i] == spj2_temp[cnt]) temp = temp+1;
    }
    answer_temp.push_back(temp);

    // 2-1.spj3(수포자3)
    cnt = 0;
    temp = 0;
    for(int i =0;i<answers.size(); i++, cnt++){
        if(i%10 == 0) cnt = 0;
        if(answers[i] == spj3_temp[cnt]) temp = temp+1;
    }
    answer_temp.push_back(temp);   

    // 3.가장 높은 점수 가진 사람 비교
    for(int i=0; i<3; i++){
        if(answer_temp[i] == *max_element(answer_temp.begin(), answer_temp.end())){
            answer.push_back(i+1);
        }         
    }

    return answer;
}
```
<br/>

## 4. 문제해결능력 UP! 되짚어보기
- vector 생성하며 동시에 초기화 가능

  \- vector 생성 : `vector<type> name();` <br/>
  \- vector의 size 정하여 생성: `vector<type> name(2);` <br/>
  \- vector 생성 및 초기화 : `vector<type> name{value1, value2, value3, ...};`
<br/><br/>

## 5. References
1) 공식 C++ References (<https://modoocode.com/241>)
<br/><br/>
