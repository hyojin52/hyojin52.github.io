---
layout: post
title: "Programmers 코딩 테스트 고득점 Kit_ [해시] 전화번호 목록"
date: 2020-03-10
categories: Programmers Hash C++
---

- 문제 유형: 해시_Key-value쌍으로 데이터를 저장하는 자료구조
- 난이도: level_02 (약 9,431명 완료)
- 사용 언어: C++ <br/><br/>

## 1. 문제
### 1) 전화번호 목록   
전화번호부에 적힌 전화번호 중, 한 번호가 다른 번호의 접두어인 경우가 있는지 확인하려 합니다.
전화번호가 다음과 같을 경우, 구조대 전화번호는 영석이의 전화번호의 접두사입니다.<br/>

- 구조대 : 119
- 박준영 : 97 674 223
- 지영석 : 11 9552 4421

전화번호부에 적힌 전화번호를 담은 배열 phone_book 이 solution 함수의 매개변수로 주어질 때, 어떤 번호가 다른 번호의 접두어인 경우가 있으면 false를 그렇지 않으면 true를 return 하도록 solution 함수를 작성해주세요.<br/>

### 2) 제한사항   
- phone_book의 길이는 1 이상 1,000,000 이하입니다.
- 각 전화번호의 길이는 1 이상 20 이하입니다.  

### 3) 기본코드
```c++
#include <string>
#include <vector>

using namespace std;

bool solution(vector<string> phone_book) {
    bool answer = true;
    return answer;
}
```
<br/><br/>

## 2. 알고리즘! 생각해보자
1) 전화번호부 오름차순 정렬하기
  - string 상태에서 정렬하게되면,  <br/>
    접두번호가 존재하는 경우) 접두번호가 제일 앞에오고, 그 뒤에 접두번호가 포함된 전화번호가 위치하게 됨

2) find() 사용해서 접두번호가 존재하는지 확인하기   
<br/><br/>

## 3. 해결코드
[C++]<br/>

```c++
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

bool solution(vector<string> phone_book) {
    bool answer = true;
    string temp = "";
    string cpy = "";   

    //1. 오름차순 정렬
    sort(phone_book.begin(), phone_book.end());

    //2. 접두번호 확인하기
    temp = phone_book[0];
    for(int i=1; i<phone_book.size(); i++){
        if(phone_book[i].find(temp) == 0){
            answer= false;
            break;
        }else{
            temp = phone_book[i];
        }
    }

    return answer;
}
```
<br/><br/>

## 4. 문제해결능력 UP! 되짚어보기
- find()함수의 return 값 : 찾고자하는 value의 index
- 해시 개념을 명확히 사용한 "map을 활용한 해결방법" 생각해보기

<br/><br/>

## 5. References
1) 공식 C++ References (<https://modoocode.com/241>)
<br/><br/>
