---
layout: post
title: "Programmers 코딩 테스트 고득점 Kit_ [Greedy] 큰 수 만들기"
date: 2020-03-26
categories: Programmers Greedy C++
toc: true
---

- 문제 유형: Greedy_부분 최적해가 전체 최적해가 되는 알고리즘
- 난이도: level_02 (약 2,169명 완료)
- 사용 언어: C++ <br/><br/>

## 1. 문제
### 1) 큰 수 만들기
어떤 숫자에서 k개의 수를 제거했을 때 얻을 수 있는 가장 큰 숫자를 구하려 합니다. 예를 들어, 숫자 1924에서 수 두 개를 제거하면 [19, 12, 14, 92, 94, 24] 를 만들 수 있습니다. 이 중 가장 큰 숫자는 94 입니다.<br/>

문자열 형식으로 숫자 number와 제거할 수의 개수 k가 solution 함수의 매개변수로 주어집니다. number에서 k 개의 수를 제거했을 때 만들 수 있는 수 중 가장 큰 숫자를 문자열 형태로 return 하도록 solution 함수를 완성하세요.
<br/>

### 2) 제한사항   
- number는 1자리 이상, 1,000,000자리 이하인 숫자입니다.
- k는 1 이상 number의 자릿수 미만인 자연수입니다.

### 3) 기본코드
```c++
#include <string>
#include <vector>

using namespace std;

string solution(string number, int k) {
    string answer = "";
    return answer;
}
```
<br/><br/>

## 2. 알고리즘! 생각해보자
Greedy -> 비교가 중요 -> 해당 문제에서는 <u>숫자 크기 비교</u> => 가장 큰 수 찾기
  - 가장 큰 수 찾기 위한 "숫자 비교 범위"는? <u>k(제거해야 할 수의 개수)+1</u> 범위에서 가장 큰 수 찾기   

1) 범위 내에서 가장 큰 수 찾기
2) 가장 큰 수 이전 숫자는 제거(동시에 ```k--```), 가장 큰 수는 answer에 append
3) 찾은 가장 큰 수 다음 수부터 범위 내에서 가장 큰 수 찾는 것 반복

number를 모두 비교하지 않았는데 k개를 모두 제거한 경우, answer의 size를 확인
예외처리 1. size가 == <u>number.size()-k</u>라면, break
예외처리 2. size가 < <u>number.size()-k</u>라면, number에서 비교되지 않은 남은 수들을 그대로 concat

<br/><br/>

## 3. 해결코드
[C++]<br/>

```c++
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

string solution(string number, int k) {
    string answer = "";

    int range_start = 0;
    int range_end = k;
    int range = number.size()-k;
    char largest;

    //1.삭제할 수 남아있으면 반복
    while(k){
        //2.가장 큰 수 찾기
        //(예외처리 1)
        if(answer.size() != range) largest = *max_element(number.begin()+range_start, number.begin()+range_end+1);
        else break;

        while(largest!=number[range_start] && k>0){
            k--;
            range_start++;
        }
        answer += number[range_start];

        range_start++;
        range_end = range_start+k;  
    }

    //(예외처리 2)
    if(answer.size() != range){
        for(int i=range_start; i<number.size(); i++){
            answer += number[i];
        }
    }

    return answer;
}
```
<br/><br/>

## 4. 문제해결능력 UP! 되짚어보기
- distance 사용한 문제해결 방법 고민해보기

<br/><br/>

## 5. References
1) [공식 C++ Reference](https://modoocode.com/241)
<br/><br/>
