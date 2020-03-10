---
layout: post
title: "Programmers 코딩 테스트 고득점 Kit_ [해시] 위장"
date: 2020-03-10
categories: Programmers Hash C++
---

- 문제 유형: 해시_Key-value쌍으로 데이터를 저장하는 자료구조
- 난이도: level_02 (약 6,880명 완료)
- 사용 언어: C++ <br/><br/>

## 1. 문제
### 1) 위장   
스파이들은 매일 다른 옷을 조합하여 입어 자신을 위장합니다.<br/>

예를 들어 스파이가 가진 옷이 아래와 같고 오늘 스파이가 동그란 안경, 긴 코트, 파란색 티셔츠를 입었다면 다음날은 청바지를 추가로 입거나 동그란 안경 대신 검정 선글라스를 착용하거나 해야 합니다.<br/>

<table border='1' bordercolor='black' width ='40%'>
  <tr style="background-color:#e3e3e3">
    <th>종류</th>
    <th>이름</th>
  </tr>
  <tr>
    <td align ="center">얼굴</td>
    <td>&nbsp;&nbsp;동그란 안경, 검정 선글라스</td>
  </tr>
  <tr>
    <td align ="center">상의</td>
    <td>&nbsp;&nbsp;파란색 티셔츠</td>
  </tr>
  <tr>
    <td align ="center">하의</td>
    <td>&nbsp;&nbsp;청바지</td>
  </tr>
  <tr>
    <td align ="center">겉옷</td>
    <td>&nbsp;&nbsp;긴 코트</td>
  </tr>
</table>


스파이가 가진 의상들이 담긴 2차원 배열 clothes가 주어질 때 서로 다른 옷의 조합의 수를 return 하도록 solution 함수를 작성해주세요.
<br/>

### 2) 제한사항   
- clothes의 각 행은 [의상의 이름, 의상의 종류]로 이루어져 있습니다.
- 스파이가 가진 의상의 수는 1개 이상 30개 이하입니다.
- 같은 이름을 가진 의상은 존재하지 않습니다.
- clothes의 모든 원소는 문자열로 이루어져 있습니다.
- 모든 문자열의 길이는 1 이상 20 이하인 자연수이고 알파벳 소문자 또는 '\_' 로만 이루어져 있습니다.
- 스파이는 하루에 최소 한 개의 의상은 입습니다.  

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
