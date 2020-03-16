---
layout: post
title: "Programmers 코딩 테스트 고득점 Kit_ [스택-큐] 쇠막대기"
date: 2020-03-15
categories: Programmers Stack-Queue C++
---

- 문제 유형: 스택-큐_LIFO-FIFO 자료형
- 난이도: level_02 (약 5,598명 완료)
- 사용 언어: C++ <br/><br/>

## 1. 문제
### 1) 쇠막대기
여러 개의 쇠막대기를 레이저로 절단하려고 합니다. 효율적인 작업을 위해서 쇠막대기를 아래에서 위로 겹쳐 놓고, 레이저를 위에서 수직으로 발사하여 쇠막대기들을 자릅니다. 쇠막대기와 레이저의 배치는 다음 조건을 만족합니다.
```
- 쇠막대기는 자신보다 긴 쇠막대기 위에만 놓일 수 있습니다.
- 쇠막대기를 다른 쇠막대기 위에 놓는 경우 완전히 포함되도록 놓되, 끝점은 겹치지 않도록 놓습니다.
- 각 쇠막대기를 자르는 레이저는 적어도 하나 존재합니다.
- 레이저는 어떤 쇠막대기의 양 끝점과도 겹치지 않습니다.
```
아래 그림은 위 조건을 만족하는 예를 보여줍니다. 수평으로 그려진 굵은 실선은 쇠막대기이고, 점은 레이저의 위치, 수직으로 그려진 점선 화살표는 레이저의 발사 방향입니다.
<img src="https://grepp-programmers.s3.amazonaws.com/files/ybm/dbd166625b/d3ae656b-bb7b-421c-9f74-fa9ea800b860.png">
이러한 레이저와 쇠막대기의 배치는 다음과 같이 괄호를 이용하여 왼쪽부터 순서대로 표현할 수 있습니다.
```
(a) 레이저는 여는 괄호와 닫는 괄호의 인접한 쌍 '()'으로 표현합니다. 또한 모든 '()'는 반드시 레이저를 표현합니다.
(b) 쇠막대기의 왼쪽 끝은 여는 괄호 '('로, 오른쪽 끝은 닫힌 괄호 ')'로 표현됩니다.
```
위 예의 괄호 표현은 그림 위에 주어져 있습니다.
쇠막대기는 레이저에 의해 몇 개의 조각으로 잘리는데, 위 예에서 가장 위에 있는 두 개의 쇠막대기는 각각 3개와 2개의 조각으로 잘리고, 이와 같은 방식으로 주어진 쇠막대기들은 총 17개의 조각으로 잘립니다.

쇠막대기와 레이저의 배치를 표현한 문자열 arrangement가 매개변수로 주어질 때, 잘린 쇠막대기 조각의 총 개수를 return 하도록 solution 함수를 작성해주세요.
<br/>

### 2) 제한사항   
- arrangement의 길이는 최대 100,000입니다.
- arrangement의 여는 괄호와 닫는 괄호는 항상 쌍을 이룹니다.

### 3) 기본코드
```c++
#include <string>
#include <vector>

using namespace std;

int solution(string arrangement) {
    int answer = 0;
    return answer;
}
```
<br/><br/>

## 2. 알고리즘! 생각해보자
1) 주어진 string arrangement에서 쇠막대기와 레이저의 인덱스를 찾기
2) 잘려진 쇠막대기 개수 구하기
  - 쇠막대기 한 개에서 잘려진 쇠막대기의 개수 = 각 쇠막대기를 통과하는 레이저 개수+1
  - 각 쇠막대기의 잘려진 쇠막대기 개수 구해서 모두 더하면 "모든 잘려진 쇠막대기 개수"

<br/><br/>

## 3. 해결코드
[C++]<br/>

```c++
#include <string>
#include <vector>
#include <stack>
#include <algorithm>

using namespace std;

int solution(string arrangement) {
    int answer = 0;

    stack<int> pipe;

    vector<int> lazer_idx;
    vector<pair<int, int>> pipe_idx;

    //1.find lazer index
    size_t found;    
    string lazer = "()";
    found = arrangement.find(lazer);

    while(found != string::npos){
        lazer_idx.push_back(found);
        found = arrangement.find(lazer, found+1);
    }

    //2.find pipe index
    for(int i=0; i<arrangement.size(); i++){
        if(arrangement.compare(i, 1, "(") == 0 && arrangement.compare(i+1, 1, ")") != 0){
            pipe.push(i);
        }
        else if(arrangement.compare(i, 1, "(") == 0 && arrangement.compare(i+1, 1, ")") == 0){
            i++;
        }
        else{
            pipe_idx.push_back(make_pair(pipe.top(), i));
            pipe.pop();
        }
    }   

    //2-1.파이프 sorting(왜? 레이저가 index 순서대로 저장되어 있으므로, 편하게 찾기 위해!)
    sort(pipe_idx.begin(), pipe_idx.end());

    //3.count lazer in each pipe, and calculate the # of cut pipes
    for(int i=0; i<pipe_idx.size(); i++){
        for(int j=0; j<lazer_idx.size(); j++){
            if(lazer_idx[j] > pipe_idx[i].first && lazer_idx[j] < pipe_idx[i].second){
                answer++;
            }
        }
        answer++;
    }

    return answer;
}
```
<br/><br/>

## 4. 문제해결능력 UP! 되짚어보기
- 만족하면서 풀었던 문제! 스택-큐 주제에 맞게 적절히 푼 것 같음
- C++ 공식 레퍼런스를 구석구석 참조해가며 문제해결!

<br/><br/>

## 5. References
1) 공식 C++ References (<https://modoocode.com/241>)
<br/><br/>
