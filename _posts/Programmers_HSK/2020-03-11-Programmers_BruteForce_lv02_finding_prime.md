---
layout: post
title: "Programmers 코딩 테스트 고득점 Kit_ [완전탐색] 소수찾기"
date: 2020-03-09
categories: Programmers BruteForce C++
---

- 문제 유형: 완전탐색_가능한 모든 상황을 조사하는 알고리즘
- 난이도: level_01 (약 9,729명 완료)
- 사용 언어: C++ <br/><br/>

## 1. 문제
### 1) 소수찾기   
한자리 숫자가 적힌 종이 조각이 흩어져있습니다. 흩어진 종이 조각을 붙여 소수를 몇 개 만들 수 있는지 알아내려 합니다.<br/>

각 종이 조각에 적힌 숫자가 적힌 문자열 numbers가 주어졌을 때, 종이 조각으로 만들 수 있는 소수가 몇 개인지 return 하도록 solution 함수를 완성해주세요.
<br/>

### 2) 제한사항   
- numbers는 길이 1 이상 7 이하인 문자열입니다.
- numbers는 0~9까지 숫자만으로 이루어져 있습니다.
- 013은 0, 1, 3 숫자가 적힌 종이 조각이 흩어져있다는 의미입니다.   

### 3) 기본코드
```c++
#include <string>
#include <vector>

using namespace std;

int solution(string numbers) {
    int answer = 0;
    return answer;
}
```
<br/>

## 2. 알고리즘! 생각해보자
1) 모든 경우의 수(2~9999999) 확인<br/>
2) 소수인지, 아닌지 확인
  - isPrime 함수 call
  - 2~sqrt(num) 범위까지 나누어지는 수 있는지 확인
  - 소수라면, numbers로 만들어질 수 있는 수 인지 확인 => answer++

<br/><br/>

## 3. 해결코드
[C++]<br/>

```c++
#include <string>
#include <vector>
#include <cmath>

using namespace std;

bool isPrime(int num){
    int end = sqrt(num);
    for(int i=2; i<=end; i++){
        if(num%i == 0) return false;
        else continue;
    }
    return true;
}

int solution(string numbers) {
    int answer = 0;
    string temp;

    //1.모든 경우의 수(2~9999999) 확인
    for(int i=2; i<=9999999; i++){
        //2.소수인지, 아닌지 확인
        if(isPrime(i)){
            //2-1.소수라면, numbers로 만들 수 있는지 확인
            temp = to_string(i);
            for(int j=0; j<numbers.size(); j++){
                if(temp.find(numbers[j]) != string::npos)
                    temp.erase(temp.find(numbers[j]), 1);
            }
            //2-2. 만들 수 있으면 answer++
            if(temp.size()==0) answer++;
        } else{
            continue;
        }
    }

    return answer;
}
```
<br/>

## 4. 문제해결능력 UP! 되짚어보기
- 완전탐색의 의미 => 2~9999999까지 모두 탐색!<br/>
- string :: erase(int index, int range);
<br/><br/>

## 5. References
1) 공식 C++ References (<https://modoocode.com/241>)
<br/><br/>
