---
layout: post
title: "Programmers 코딩 테스트 고득점 Kit_ [Greedy] 조이스틱"
date: 2020-03-21
categories: Programmers Greedy C++
toc: true
---

- 문제 유형: Greedy_부분 최적해가 전체 최적해가 되는 알고리즘
- 난이도: level_02 (약 1,649명 완료)
- 사용 언어: C++ <br/><br/>

## 1. 문제
### 1) 조이스틱
조이스틱으로 알파벳 이름을 완성하세요. 맨 처음엔 A로만 이루어져 있습니다.<br/>
ex) 완성해야 하는 이름이 세 글자면 AAA, 네 글자면 AAAA

조이스틱을 각 방향으로 움직이면 아래와 같습니다.
```
▲ - 다음 알파벳
▼ - 이전 알파벳 (A에서 아래쪽으로 이동하면 Z로)
◀ - 커서를 왼쪽으로 이동 (첫 번째 위치에서 왼쪽으로 이동하면 마지막 문자에 커서)
▶ - 커서를 오른쪽으로 이동
```

예를 들어 아래의 방법으로 JAZ를 만들 수 있습니다.
```
- 첫 번째 위치에서 조이스틱을 위로 9번 조작하여 J를 완성합니다.
- 조이스틱을 왼쪽으로 1번 조작하여 커서를 마지막 문자 위치로 이동시킵니다.
- 마지막 위치에서 조이스틱을 아래로 1번 조작하여 Z를 완성합니다.
따라서 11번 이동시켜 "JAZ"를 만들 수 있고, 이때가 최소 이동입니다.
```

만들고자 하는 이름 name이 매개변수로 주어질 때, 이름에 대해 조이스틱 조작 횟수의 최솟값을 return 하도록 solution 함수를 만드세요.
<br/>

### 2) 제한사항   
- name은 알파벳 대문자로만 이루어져 있습니다.
- name의 길이는 1 이상 20 이하입니다.

### 3) 기본코드
```c++
#include <string>
#include <vector>

using namespace std;

int solution(string name) {
    int answer = 0;
    return answer;
}
```
<br/><br/>

## 2. 알고리즘! 생각해보자
"각 알파벳의 최소 커서이동, 최소 알파벳 변경되는 경우를 찾자!"

1) 최소 알파벳 변경되는 경우: A에서 해당 알파벳까지 거리, Z에서 해당 알파벳까지 거리 비교
2) 최소 커서이동되는 경우: forward 및 backward 방향 거리 비교(단, 예외상황 처리)
  - 'A'가 처음에 연속으로 나오는 경우
  - 문자열이 마지막에 AA***로 끝나고, 마지막 커서이동이 backward로 이루어진 경우

<br/><br/>

## 3. 해결코드
[C++]<br/>

```c++
#include <string>
#include <vector>

using namespace std;

int solution(string name) {
    int answer = 0;

    int a_cnt = 0;
    int forward, backward;
    bool back = false;

    for(int i=0; i<name.size(); i++){     

        if(name[i] !='A'){

            //1.최소 알파벳 변경되는 경우
            if((int)name[i]-'A' <= (int)'Z'-name[i]+1){
                answer += (int)name[i]-'A';
            }
            else{
                answer += (int)'Z'-name[i]+1;
            }

            //2.최소 커서이동되는 경우
            //(예외 처리) 'A'가 처음에 연속으로 나오는 경우
            if(i == a_cnt){
                forward = a_cnt;
                backward = 1;
            }
            else{
                forward = 1+a_cnt;
                backward = i-a_cnt;
            }

            if(backward < forward){
                answer += backward;
                back = true;
            }
            else{
                answer += forward;
                back = false;
            }

            a_cnt = 0;
        }
        else{
            a_cnt++;
        }
    }

    //(예외처리) 문자열이 마지막에 AA***로 끝나고, 마지막 커서이동이 backward로 이루어진 경우
    if(back && a_cnt>0){
        answer += a_cnt;
    }

    return answer;
}

```
<br/><br/>

## 4. 문제해결능력 UP! 되짚어보기
- 과연 이 문제가 Greedy 알고리즘에 해당하는 문제일까?
  (부분 최적해가 전체 최적해가 되지 않은 것 같은데...)

<br/><br/>

## 5. References
1) [좀 더 현명한 해결책](https://0pencoding.github.io/%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%A8%B8%EC%8A%A4%EA%B3%A0%EB%93%9D%EC%A0%90kit/greedy/level2/algorithm/c++/2020/03/21/%ED%83%90%EC%9A%95%EB%B2%95_%EC%A1%B0%EC%9D%B4%EC%8A%A4%ED%8B%B1_level2.html)<br/>
2) [공식 C++ Reference](https://modoocode.com/241)
<br/><br/>
