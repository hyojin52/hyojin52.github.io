---
layout: post
title: "Programmers 코딩 테스트 고득점 Kit_ [정렬] H-index"
date: 2020-03-08
categories: Programmers Sort C++
---

- 문제 유형: 정렬_자료를 일정한 규칙에 따라 나열하는 것
- 난이도: level_02 (약 4,326명 완료)
- 사용 언어: C++ <br/><br/>

## 1. 문제
### 1) K번째수
H-Index는 과학자의 생산성과 영향력을 나타내는 지표입니다. 어느 과학자의 H-Index를 나타내는 값인 h를 구하려고 합니다. 위키백과1에 따르면, H-Index는 다음과 같이 구합니다.<br/>

어떤 과학자가 발표한 논문 n편 중, h번 이상 인용된 논문이 h편 이상이고 나머지 논문이 h번 이하 인용되었다면 h가 이 과학자의 H-Index입니다.<br/>

어떤 과학자가 발표한 논문의 인용 횟수를 담은 배열 citations가 매개변수로 주어질 때, 이 과학자의 H-Index를 return 하도록 solution 함수를 작성해주세요.
<br/>

### 2) 제한사항   
- 과학자가 발표한 논문의 수는 1편 이상 1,000편 이하입니다.
- 논문별 인용 횟수는 0회 이상 10,000회 이하입니다.   

### 3) 기본코드
```c++
#include <string>
#include <vector>

using namespace std;

int solution(vector<int> citations) {
    int answer = 0;   
    return answer;
}
```
<br/>

## 2. 알고리즘! 생각해보자
1) h-index 조건
  - h번 이상 인용된 논문이 h편 이상
  - 나머지 논문이 h번 이하 인용

=> (서로 교집합이 없는 조건) 둘 중 하나만 만족하면 됨, <u>첫번째 조건</u> 활용<br/><br/>
2) h-index의 범위는 "0 ~ 논문의 개수" -> 반복문 활용해서 찾기<br/>
  - h번 이상 인용된 논문 개수 count
  -  불필요한 반복문(=논문의 개수를 넘었을 때) break

<br/><br/>

## 3. 해결코드
[C++]<br/>

```c++
#include <string>
#include <vector>

using namespace std;

int solution(vector<int> citations) {
    int answer = 0;    
    int candidate;

    //2.h-index의 범위는 "0 ~ 논문의 개수" -> 반복문 활용해서 찾기
    for(int i=0; i<=citations.size(); i++){
        //2-1.h번 이상 인용된 논문 개수 count
        candidate = 0;
        for(int j=0; j<citations.size(); j++){
            if(i<=citations[j])
              candidate++;
        }

        //2-2.불필요한 반복문 break
        if(i>candidate) break;
        else answer = i;    
    }    
    return answer;
}
```  
<br/><br/>

## 4. 문제해결능력 UP! 되짚어보기
- H-index에 대한 이해가 필요
- 다양한 test case를 고려하여 프로그래밍하기
  ({47,31,24,1}:h-index 3, {4,3,3}:h-index 3 등)
- 단순하고 직관적인 코드 작성하도록 노력하기

<br/><br/>

## 5. References
1)  공식 C++ References (<https://modoocode.com/241>)
<br/><br/>
