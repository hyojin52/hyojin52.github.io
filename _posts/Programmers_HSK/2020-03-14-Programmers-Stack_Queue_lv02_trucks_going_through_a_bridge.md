---
layout: post
title: "Programmers 코딩 테스트 고득점 Kit_ [스택-큐] 다리를 지나는 트럭"
date: 2020-03-14
categories: Programmers Stack-Queue C++
---

- 문제 유형: 스택-큐_LIFO-FIFO 자료형
- 난이도: level_02 (약 4,755명 완료)
- 사용 언어: C++ <br/><br/>

## 1. 문제
### 1) 다리를 지나는 트럭   
트럭 여러 대가 강을 가로지르는 일 차선 다리를 정해진 순으로 건너려 합니다. 모든 트럭이 다리를 건너려면 최소 몇 초가 걸리는지 알아내야 합니다. 트럭은 1초에 1만큼 움직이며, 다리 길이는 bridge_length이고 다리는 무게 weight까지 견딥니다.<br/>
※ 트럭이 다리에 완전히 오르지 않은 경우, 이 트럭의 무게는 고려하지 않습니다.<br/>

예를 들어, 길이가 2이고 10kg 무게를 견디는 다리가 있습니다. 무게가 [7, 4, 5, 6]kg인 트럭이 순서대로 최단 시간 안에 다리를 건너려면 다음과 같이 건너야 합니다.<br/>
<table border='1' bordercolor='black' width ='60%'>
  <tr style="background-color:#e3e3e3">
    <th>경과 시간</th>
    <th>다리를 지난 트럭</th>
    <th>다리를 건너는 트럭</th>
    <th>대기 트럭</th>
  </tr>
  <tr>
    <td align ="center">0</td>
    <td align ="center">[]</td>
    <td align ="center">[]</td>
    <td align ="center">[7,4,5,6]</td>
  </tr>
  <tr>
    <td align ="center">1~2</td>
    <td align ="center">[]</td>
    <td align ="center">[7]</td>
    <td align ="center">[4,5,6]</td>
  </tr>
  <tr>
    <td align ="center">3</td>
    <td align ="center">[7]</td>
    <td align ="center">[4]</td>
    <td align ="center">[5,6]</td>
  </tr>
  <tr>
    <td align ="center">4</td>
    <td align ="center">[7]</td>
    <td align ="center">[4,5]</td>
    <td align ="center">[6]</td>
  </tr>
  <tr>
    <td align ="center">5</td>
    <td align ="center">[7,4]</td>
    <td align ="center">[5]</td>
    <td align ="center">[6]</td>
  </tr>
  <tr>
    <td align ="center">6~7</td>
    <td align ="center">[7,4,5]</td>
    <td align ="center">[6]</td>
    <td align ="center">[]</td>
  </tr>
  <tr>
    <td align ="center">8</td>
    <td align ="center">[7,4,5,6]</td>
    <td align ="center">[]</td>
    <td align ="center">[]</td>
  </tr>
</table>

따라서, 모든 트럭이 다리를 지나려면 최소 8초가 걸립니다.<br/>

solution 함수의 매개변수로 다리 길이 bridge_length, 다리가 견딜 수 있는 무게 weight, 트럭별 무게 truck_weights가 주어집니다. 이때 모든 트럭이 다리를 건너려면 최소 몇 초가 걸리는지 return 하도록 solution 함수를 완성하세요.
<br/>

### 2) 제한사항   
- bridge_length는 1 이상 10,000 이하입니다.
- weight는 1 이상 10,000 이하입니다.
- truck_weights의 길이는 1 이상 10,000 이하입니다.
- 모든 트럭의 무게는 1 이상 weight 이하입니다.  

### 3) 기본코드
```c++
#include <string>
#include <vector>

using namespace std;

int solution(int bridge_length, int weight, vector<int> truck_weights) {
    int answer = 0;
    return answer;
}
```
<br/><br/>

## 2. 알고리즘! 생각해보자
1) 문제처럼 다리 지나는 트럭(run_truck), 다리를 지난 트럭(ran_truck) 사용<br/>
2) 모든 트럭이 다리를 지날 때(```ran_truck.size() == truck_weights.size()```)까지 아래를 반복
  - 시간 1초씩 증가
  - 달리고 있는 트럭이 없으면, 트럭 추가
  - 달리고 있는 트럭이 있으면, 트럭 전진&다리 전부 건넜는지 확인/트럭 더 추가할 수 있는지 확인

<br/><br/>

## 3. 해결코드
[C++]<br/>

```c++
#include <string>
#include <vector>

using namespace std;

int solution(int bridge_length, int weight, vector<int> truck_weights) {
    int answer = 0;

    vector<int> run_truck, ran_truck;
    int now_weight = 0;
    int i=0;

    //1. 트럭이 모두 지나면 answer(시간) count 멈추기
    while(ran_truck.size() != truck_weights.size()){
        //1-1.반복문 돌때마다 시간 1초 증가
        answer++;

        //1-2.달리고 있는 트럭이 없으면, 트럭 추가
        if(run_truck.size() == 0){
            now_weight += truck_weights[i];
            if(i+1 != truck_weights.size()) i++;
            run_truck.push_back(0);
        }
        //1-3.달리고 있는 트럭이 있으면,
        else{
            for(int j=0; j<run_truck.size(); j++){
                //1-3-1.트럭 1만큼 전진
                run_truck[j]++;
                //1-3-2.달리고 있는 트럭 다리 건넜는지 확인
                if(run_truck[j] == bridge_length){
                    run_truck.erase(run_truck.begin()+j);
                    j--;
                    ran_truck.push_back(truck_weights[ran_truck.size()]);
                    now_weight -= truck_weights[ran_truck.size()-1];
                }


            }

            //1-3-3.트럭 더 추가할 수 있는지 확인
            if(i <truck_weights.size() && now_weight+truck_weights[i] <= weight){
                now_weight += truck_weights[i++];
                run_truck.push_back(0);
            }
        }
    }

    return answer;
}
```
<br/><br/>

## 4. 문제해결능력 UP! 되짚어보기
- 이것이 과연 스택-큐 문제인가... 내가 잘못된 방향으로 푼것인가... **"스택-큐"** 사용해서도 풀어보자!

<br/><br/>

## 5. References
1) 공식 C++ References (<https://modoocode.com/241>)
<br/><br/>
