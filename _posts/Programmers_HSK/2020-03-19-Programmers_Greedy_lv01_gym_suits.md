---
layout: post
title: "Programmers 코딩 테스트 고득점 Kit_ [Greedy] 체육복"
date: 2020-03-19
categories: Programmers Greedy C++
---

- 문제 유형: Greedy_부분 최적해가 전체 최적해가 되는 알고리즘
- 난이도: level_01 (약 6,180명 완료)
- 사용 언어: C++ <br/><br/>

## 1. 문제
### 1) 체육복
점심시간에 도둑이 들어, 일부 학생이 체육복을 도난당했습니다. 다행히 여벌 체육복이 있는 학생이 이들에게 체육복을 빌려주려 합니다. 학생들의 번호는 체격 순으로 매겨져 있어, 바로 앞번호의 학생이나 바로 뒷번호의 학생에게만 체육복을 빌려줄 수 있습니다. 예를 들어, 4번 학생은 3번 학생이나 5번 학생에게만 체육복을 빌려줄 수 있습니다. 체육복이 없으면 수업을 들을 수 없기 때문에 체육복을 적절히 빌려 최대한 많은 학생이 체육수업을 들어야 합니다.<br/>

전체 학생의 수 n, 체육복을 도난당한 학생들의 번호가 담긴 배열 lost, 여벌의 체육복을 가져온 학생들의 번호가 담긴 배열 reserve가 매개변수로 주어질 때, 체육수업을 들을 수 있는 학생의 최댓값을 return 하도록 solution 함수를 작성해주세요.
<br/>

### 2) 제한사항   
- 전체 학생의 수는 2명 이상 30명 이하입니다.
- 체육복을 도난당한 학생의 수는 1명 이상 n명 이하이고 중복되는 번호는 없습니다.
- 여벌의 체육복을 가져온 학생의 수는 1명 이상 n명 이하이고 중복되는 번호는 없습니다.
- 여벌 체육복이 있는 학생만 다른 학생에게 체육복을 빌려줄 수 있습니다.
- 여벌 체육복을 가져온 학생이 체육복을 도난당했을 수 있습니다. 이때 이 학생은 체육복을 하나만 도난당했다고 가정하며, 남은 체육복이 하나이기에 다른 학생에게는 체육복을 빌려줄 수 없습니다.

### 3) 기본코드
```c++
#include <string>
#include <vector>

using namespace std;

int solution(int n, vector<int> lost, vector<int> reserve) {
    int answer = 0;
    return answer;
}
```
<br/><br/>

## 2. 알고리즘! 생각해보자
1) 체육복을 잃어버린 학생들 = n-lost.size()<br/>
2) 여분 체육복 가지고 왔는데 잃어버린 학생들 확인<br/>
3) 잃어버린 학생이 앞 or 뒤 번호 학생들에게 체육복 빌릴 수 있는지 확인
<br/><br/>

## 3. 해결코드
[C++]<br/>

```c++
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

int solution(int n, vector<int> lost, vector<int> reserve) {
    //1.체육복을 잃어버린 학생들 = n-lost.size()
    int answer = n-lost.size();

    vector<int>::iterator it;   

    //2.여분 체육복 가지고 왔는데 잃어버린 학생들 확인
    for(int i=0; i<lost.size(); i++){
        it = find(reserve.begin(), reserve.end(), lost[i]);
        if(it != reserve.end()){
            answer++;
            reserve.erase(it);
            lost.erase(lost.begin()+i);
            i--;
        }
    }

    //3.잃어버린 학생이 앞 or 뒤 번호 학생들에게 체육복 빌릴 수 있는지 확인
    for(int i=0; i<lost.size(); i++){
        if(reserve.size() == 0) break;

        it = find(reserve.begin(), reserve.end(), lost[i]-1);
        if(it != reserve.end()){
            answer++;
            reserve.erase(it);
            continue;
        }

        it = find(reserve.begin(), reserve.end(), lost[i]+1);
        if(it != reserve.end()){
            answer++;
            reserve.erase(it);
        }
    }  

    return answer;
}
```
<br/><br/>

## 4. 문제해결능력 UP! 되짚어보기
- ```vector<int> lost``` 의 원소를 삭제하지 않고 문제 해결하기

<br/><br/>

## 5. References
1) Greedy 알고리즘 (<https://www.zerocho.com/category/Algorithm/post/584ba5c9580277001862f188>)
2) 공식 C++ References (<https://modoocode.com/241>)
<br/><br/>
