---
layout: post
title: "Programmers 코딩 테스트 고득점 Kit_ [힙] 라면공장"
date: 2020-03-17
categories: Programmers Heap C++
---

- 문제 유형: 힙_검색에 특화된 자료구조
- 난이도: level_02 (약 1,902명 완료)
- 사용 언어: C++ <br/><br/>

## 1. 문제
### 1) 라면공장
라면 공장에서는 하루에 밀가루를 1톤씩 사용합니다. 원래 밀가루를 공급받던 공장의 고장으로 앞으로 k일 이후에야 밀가루를 공급받을 수 있기 때문에 해외 공장에서 밀가루를 수입해야 합니다. 해외 공장에서는 향후 밀가루를 공급할 수 있는 날짜와 수량을 알려주었고, 라면 공장에서는 운송비를 줄이기 위해 최소한의 횟수로 밀가루를 공급받고 싶습니다.<br/>

현재 공장에 남아있는 밀가루 수량 stock, 밀가루 공급 일정(dates)과 해당 시점에 공급 가능한 밀가루 수량(supplies), 원래 공장으로부터 공급받을 수 있는 시점 k가 주어질 때, 밀가루가 떨어지지 않고 공장을 운영하기 위해서 최소한 몇 번 해외 공장으로부터 밀가루를 공급받아야 하는지를 return 하도록 solution 함수를 완성하세요.<br/>

dates[i]에는 i번째 공급 가능일이 들어있으며, supplies[i]에는 dates[i] 날짜에 공급 가능한 밀가루 수량이 들어 있습니다.
<br/>

### 2) 제한사항   
- stock에 있는 밀가루는 오늘(0일 이후)부터 사용됩니다.
- stock과 k는 2 이상 100,000 이하입니다.
- dates의 각 원소는 1 이상 k 이하입니다.
- supplies의 각 원소는 1 이상 1,000 이하입니다.
- dates와 supplies의 길이는 1 이상 20,000 이하입니다.
- k일 째에는 밀가루가 충분히 공급되기 때문에 k-1일에 사용할 수량까지만 확보하면 됩니다.
- dates에 들어있는 날짜는 오름차순 정렬되어 있습니다.
- dates에 들어있는 날짜에 공급되는 밀가루는 작업 시작 전 새벽에 공급되는 것을 기준으로 합니다. 예를 들어 9일째에 밀가루가 바닥나더라도, 10일째에 공급받으면 10일째에는 공장을 운영할 수 있습니다.
- 밀가루가 바닥나는 경우는 주어지지 않습니다.

### 3) 기본코드
```c++
#include <string>
#include <vector>

using namespace std;

int solution(int stock, vector<int> dates, vector<int> supplies, int k) {
    int answer = 0;
    return answer;
}
```
<br/><br/>

## 2. 알고리즘! 생각해보자
방법 1. (해결코드에서 사용한 방법)<br/>
"<u>최대로 공급할 수 있는 양을 찾아 공급한다면 최소로 공급받을 수 있음</u>"<br/>
이 때, 공급량 비교할 dates를 어떻게 구분할까?<br/>
=> K개 밀가루를 공급받지 못했다면, (반복)현재 stock 내에서 공급받을 수 있는 모든 날짜들 확인해서 최대로 공급할 수 있는 양을 찾기<br/>

방법 2.
"<u>최대로 공급할 수 있는 양을 찾아 공급한다면 최소로 공급받을 수 있음</u>"<br/>
K일이 될 때까지 매일 <u>아래 루틴</u>을 반복
- stock 1 씩 감소

- 공급받을 수 있는 날이 되면 공급량 heap에 추가
-  만약 stock이 0이 되면, heap에서 top만큼 추가해주고 heap에서 삭제

<br/><br/>

## 3. 해결코드
[C++]<br/>

```c++
#include <string>
#include <vector>
#include <queue>

using namespace std;

int solution(int stock, vector<int> dates, vector<int> supplies, int k) {
    int answer = 0;

    priority_queue<int> prediction;

    //1. K개 밀가루를 공급받지 못했다면, 아래 반복
    int dates_idx = 0;  
    while(stock < k){
        // 2. 현재 stock 내에서 공급받을 수 있는 모든 공급량들 힙에 넣기
        while(dates[dates_idx] <= stock && dates_idx < dates.size()){
            prediction.push(supplies[dates_idx++]);
        }
        //3.max heap에서 최대로 공급할 수 있는 양(root의 값)을 stock에 추가
        stock += prediction.top();
        prediction.pop();

        //4. 공급받았으니 asnwer 증가
        answer++;
    }

    return answer;
}
```
<br/><br/>

## 4. 문제해결능력 UP! 되짚어보기
- 여러가지 방법으로 해결해보기(방법 2.등)
<br/><br/>

## 5. References
1) Heap 개념 (<https://reakwon.tistory.com/42>)
2) C++ Heap 구현 (<https://twpower.github.io/137-heap-implementation-in-cp>)
3) C++ heap과 관련된 함수 (<https://openmynotepad.tistory.com/35>)
2) 공식 C++ References (<https://modoocode.com/241>)
<br/><br/>
