---
layout: post
title: "Programmers 코딩 테스트 고득점 Kit_ [Greedy] 구명보트"
date: 2020-03-28
categories: Programmers Greedy C++
toc: true
---

- 문제 유형: Greedy_부분 최적해가 전체 최적해가 되는 알고리즘
- 난이도: level_02 (약 2,037명 완료)
- 사용 언어: C++ <br/><br/>

## 1. 문제
### 1) 구명보트
무인도에 갇힌 사람들을 구명보트를 이용하여 구출하려고 합니다. 구명보트는 작아서 한 번에 최대 2명씩 밖에 탈 수 없고, 무게 제한도 있습니다. 예를 들어, 사람들의 몸무게가 [70kg, 50kg, 80kg, 50kg]이고 구명보트의 무게 제한이 100kg이라면 2번째 사람과 4번째 사람은 같이 탈 수 있지만 1번째 사람과 3번째 사람의 무게의 합은 150kg이므로 구명보트의 무게 제한을 초과하여 같이 탈 수 없습니다.<br/>

구명보트를 최대한 적게 사용하여 모든 사람을 구출하려고 합니다. 사람들의 몸무게를 담은 배열 people과 구명보트의 무게 제한 limit가 매개변수로 주어질 때, 모든 사람을 구출하기 위해 필요한 구명보트 개수의 최솟값을 return 하도록 solution 함수를 작성해주세요.
<br/>

### 2) 제한사항   
- 무인도에 갇힌 사람은 1명 이상 50,000명 이하입니다.
- 각 사람의 몸무게는 40kg 이상 240kg 이하입니다.
- 구명보트의 무게 제한은 40kg 이상 240kg 이하입니다.
- 구명보트의 무게 제한은 항상 사람들의 몸무게 중 최댓값보다 크게 주어지므로 사람들을 구출할 수 없는 경우는 없습니다.

### 3) 기본코드
```c++
#include <string>
#include <vector>

using namespace std;

int solution(vector<int> people, int limit) {
    int answer = 0;
    return answer;
}
```
<br/><br/>

## 2. 알고리즘! 생각해보자
핵심 알고리즘 : 무게 제한에 따라 1인 or 2인 탑승할 것인지 결정

1) people을 내림차순으로 정렬<br/>
2) 최대 무게의 사람부터 1인 or 2인 탑승할 것인지 결정
  - How to? 가장 뒤의 사람(가장 가벼운 사람)과 같이 탑승할 수 있는지 확인
  - 같이 탈 수 있다면, 가장 뒤의 사람 지우기 (2인 탑승)
  - 같이 탈 수 없다면, continue(1인 탑승)
  
3) 탑승 종류 결정 이후 answer++

<br/><br/>

## 3. 해결코드
[C++]<br/>

```c++
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

int solution(vector<int> people, int limit) {
    int answer = 0;
    int temp;

    sort(people.begin(), people.end(), greater<int>());

    for(int i=0; i<people.size(); i++){
        temp = people[i];
        if(temp+people.back()<=limit) people.erase(people.end()-1);
        answer++;
    }

    return answer;
}
```
<br/><br/>

## 4. 문제해결능력 UP! 되짚어보기
- greedy로 문제 해결시, <u>비교해야 할 것</u>을 정확히 정하기

<br/><br/>

## 5. References
1) [공식 C++ Reference](https://modoocode.com/241)
<br/><br/>
