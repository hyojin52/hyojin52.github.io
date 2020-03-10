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
1) multimap, set 자료구조("key, value" pair) 사용<br/>
2) multimap, set 초기화<br/>
3) 경우의 수 계산<br/>
<br/><br/>

## 3. 해결코드
[C++]<br/>

```c++
#include <string>
#include <vector>
#include <map>
#include <set>

using namespace std;

int solution(vector<vector<string>> clothes) {
    int answer = 1;

    // 1.set, multipmap 초기화(clothes 벡터 이용)
    multimap<string, string> c_temp;
    set<string> key;
    set<string>::iterator iter;

    for(int i=0; i<clothes.size(); i++){
        c_temp.insert(pair<string, string>(clothes[i][1], clothes[i][0]));
        key.insert(clothes[i][1]);
    }

    // 2.의상 조합 경우의 수 계산
    for(iter=key.begin(); iter != key.end(); ++iter){
        answer = answer*(c_temp.count(*iter)+1);
    }
    answer = answer-1;

    return answer;
}
```
<br/><br/>

## 4. 문제해결능력 UP! 되짚어보기
- 의상 조합 경우의 수 계산_ 단순하게 생각하기!
- map과 set의 연관성 생각해보기<br/>
  \- map: key와 value pair<br/>
  \- set: key 값들

<br/><br/>

## 5. References
1) 공식 C++ References (<https://modoocode.com/241>)
<br/><br/>
