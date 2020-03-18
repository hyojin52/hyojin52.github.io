---
layout: post
title: "Programmers 코딩 테스트 고득점 Kit_ [힙] 더맵게"
date: 2020-03-17
categories: Programmers Heap C++
---

- 문제 유형: 힙_검색에 특화된 자료구조
- 난이도: level_02 (약 4,292명 완료)
- 사용 언어: C++ <br/><br/>

## 1. 문제
### 1) 더 맵게
매운 것을 좋아하는 Leo는 모든 음식의 스코빌 지수를 K 이상으로 만들고 싶습니다. 모든 음식의 스코빌 지수를 K 이상으로 만들기 위해 Leo는 스코빌 지수가 가장 낮은 두 개의 음식을 아래와 같이 특별한 방법으로 섞어 새로운 음식을 만듭니다.<br/>
 ```c++
 섞은 음식의 스코빌 지수 = 가장 맵지 않은 음식의 스코빌 지수 + (두 번째로 맵지 않은 음식의 스코빌 지수 * 2)
 ```
Leo는 모든 음식의 스코빌 지수가 K 이상이 될 때까지 반복하여 섞습니다. Leo가 가진 음식의 스코빌 지수를 담은 배열 scoville과 원하는 스코빌 지수 K가 주어질 때, 모든 음식의 스코빌 지수를 K 이상으로 만들기 위해 섞어야 하는 최소 횟수를 return 하도록 solution 함수를 작성해주세요.
<br/>

### 2) 제한사항   
- scoville의 길이는 1 이상 1,000,000 이하입니다.
- K는 0 이상 1,000,000,000 이하입니다.
- scoville의 원소는 각각 0 이상 1,000,000 이하입니다.
- 모든 음식의 스코빌 지수를 K 이상으로 만들 수 없는 경우에는 -1을 return 합니다.

### 3) 기본코드
```c++
#include <string>
#include <vector>

using namespace std;

int solution(vector<int> scoville, int K) {
    int answer = 0;
    return answer;
}
```
<br/><br/>

## 2. 알고리즘! 생각해보자
min heap 사용해서 제일 낮은 맵기인 음식 찾아서 새로운 읍식 만들기<br/>
1) min heap 생성<br/>
2) 스코빌 지수가 "K 미만"이라면 아래를 반복
  - 스코빌지수 가장 낮은 두 개 음식 섞어 새로운 음식 만들기
  - 새로운 음식 추가

3) K이상의 스코빌 지수를 만들 수 없다면, -1 제작
<br/><br/>

## 3. 해결코드
[C++]<br/>

```c++
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

int solution(vector<int> scoville, int K) {
    int answer = scoville.size();

    //1.min heap 만들기
    make_heap(scoville.begin(), scoville.end(), greater<int>());

    //2.스코빌 지수가 "K 미만"이라면 아래를 반복
    int new_food;
    while(scoville.front() < K && scoville.size() > 1){

        //2-1.스코빌지수 가장 낮은 두 개 음식 섞어 새로운 음식 만들기
        pop_heap(scoville.begin(), scoville.end(), greater<int>());        
        new_food = scoville.back();
        scoville.pop_back();
        pop_heap(scoville.begin(), scoville.end(), greater<int>());        
        new_food += scoville.back()*2;
        scoville.pop_back();

        //2-2. 새로운 음식 추가
        scoville.push_back(new_food);
        push_heap(scoville.begin(), scoville.end(), greater<int>());
    }

    if(scoville.size() <= 1 && scoville.front() < K) answer = -1;
    else answer -= scoville.size();

    return answer;
}
```
<br/><br/>

## 4. 문제해결능력 UP! 되짚어보기
- 문제를 읽으면서 풀이법을 연상할 수 있어 빠른 시간 내에 해결할 수 있었던 문제!
<br/><br/>

## 5. References
1) Heap 개념 (<https://reakwon.tistory.com/42>)
2) C++ Heap 구현 (<https://twpower.github.io/137-heap-implementation-in-cp>)
3) C++ heap과 관련된 함수 (<https://openmynotepad.tistory.com/35>)
2) 공식 C++ References (<https://modoocode.com/241>)
<br/><br/>
