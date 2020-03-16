---
layout: post
title: "Programmers 코딩 테스트 고득점 Kit_ [스택-큐] 프린터"
date: 2020-03-14
categories: Programmers Stack-Queue C++
---

- 문제 유형: 스택-큐_LIFO-FIFO 자료형
- 난이도: level_02 (약 6,210명 완료)
- 사용 언어: C++ <br/><br/>

## 1. 문제
### 1) 프린터
일반적인 프린터는 인쇄 요청이 들어온 순서대로 인쇄합니다. 그렇기 때문에 중요한 문서가 나중에 인쇄될 수 있습니다. 이런 문제를 보완하기 위해 중요도가 높은 문서를 먼저 인쇄하는 프린터를 개발했습니다. 이 새롭게 개발한 프린터는 아래와 같은 방식으로 인쇄 작업을 수행합니다.<br/>
```
1. 인쇄 대기목록의 가장 앞에 있는 문서(J)를 대기목록에서 꺼냅니다.
2. 나머지 인쇄 대기목록에서 J보다 중요도가 높은 문서가 한 개라도 존재하면 J를 대기목록의 가장 마지막에 넣습니다.
3. 그렇지 않으면 J를 인쇄합니다.
```
예를 들어, 4개의 문서(A, B, C, D)가 순서대로 인쇄 대기목록에 있고 중요도가 2 1 3 2 라면 C D A B 순으로 인쇄하게 됩니다. 내가 인쇄를 요청한 문서가 몇 번째로 인쇄되는지 알고 싶습니다. 위의 예에서 C는 1번째로, A는 3번째로 인쇄됩니다.<br/>

현재 대기목록에 있는 문서의 중요도가 순서대로 담긴 배열 priorities와 내가 인쇄를 요청한 문서가 현재 대기목록의 어떤 위치에 있는지를 알려주는 location이 매개변수로 주어질 때, 내가 인쇄를 요청한 문서가 몇 번째로 인쇄되는지 return 하도록 solution 함수를 작성해주세요.
<br/>

### 2) 제한사항   
- 현재 대기목록에는 1개 이상 100개 이하의 문서가 있습니다.
- 인쇄 작업의 중요도는 1~9로 표현하며 숫자가 클수록 중요하다는 뜻입니다.
- location은 0 이상 (현재 대기목록에 있는 작업 수 - 1) 이하의 값을 가지며 대기목록의 가장 앞에 있으면 0, 두 번째에 있으면 1로 표현합니다.

### 3) 기본코드
```c++
#include <string>
#include <vector>

using namespace std;

int solution(vector<int> priorities, int location) {
    int answer = 0;
    return answer;
}
```
<br/><br/>

## 2. 알고리즘! 생각해보자
1) 각 문서가 몇 번째에 출력되는지 계산 => priorities 자체를 변경하기 보다 <u>다른 공간</u>(:: ```vector<int> document;```)을 사용하자!
  - priorities와 document의 관계 : document에 priorities의 index 저장 -> document 통해서 priorities 접근!
  - ex) priorities[0] == priorities[document[0]]

<div style="width:50%;float:left;block:inline-block;padding-left:20px;">
  priorities
  <table border='1' bordercolor='black' width ='60%'>
    <tr>
      <th style="background-color:#e3e3e3;font-size:13px;padding:5px;">index</th>
      <td align ="center" style="padding:5px;">0</td>
      <td align ="center" style="padding:5px;">1</td>
      <td align ="center" style="padding:5px;">2</td>
      <td align ="center" style="padding:5px;">3</td>      
    </tr>
    <tr>
      <th style="background-color:#e3e3e3;font-size:13px;padding:5px;">value<br/>(priority)</th>
      <td align ="center" style="padding:5px;">2</td>
      <td align ="center" style="padding:5px;">1</td>
      <td align ="center" style="padding:5px;">3</td>
      <td align ="center" style="padding:5px;">2</td>
    </tr>
  </table>
</div>
<div style="width:50%;float:left;block:inline-block;">  
  document
  <table border='1' bordercolor='black' width ='60%'>
    <tr>
      <th style="background-color:#e3e3e3;font-size:13px;padding:5px;">index</th>
      <td align ="center" style="padding:5px;">0</td>
      <td align ="center" style="padding:5px;">1</td>
      <td align ="center" style="padding:5px;">2</td>
      <td align ="center" style="padding:5px;">3</td>      
    </tr>
    <tr>
      <th style="background-color:#e3e3e3;font-size:13px;padding:5px;">value<br/>(priority)</th>
      <td align ="center" style="padding:5px;">0</td>
      <td align ="center" style="padding:5px;">1</td>
      <td align ="center" style="padding:5px;">2</td>
      <td align ="center" style="padding:5px;">3</td>
    </tr>
  </table>
</div>
<ul style="color:white;"><ol>white space</ol></ul>

2) location에 있는 문서가 출력될 때까지 <u>"아래" 반복</u>
  - location에 있는 문서가 출력되면 stop
  - 우선순위가 더 높은 문서가 있다면, 맨 뒤로 보내기
  - 우선순위가 더 높은 문서가 없다면(=자신이 우선순위가 제일 높다면), 출력&최고 우선순위 저장

<br/><br/>

## 3. 해결코드
[C++]<br/>

```c++
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

int solution(vector<int> priorities, int location) {
    int answer = 0;

    vector<int> document;
    int max;

    //1-1.document 초기화
    for(int i=0; i<priorities.size(); i++){
        document.push_back(i);
    }
    //1-2.가장 높은 우선순위 저장
    max = *(max_element(priorities.begin(), priorities.end()));

    //2.location 위치에 있는 문서가 출력될 때까지 반복
    while(true){

        //2-1.location에 있는 문서가 출력되면 stop
        if(document[0] == location && priorities[document[0]] == max){
            answer++;
            break;
        }

        //2-2.우선순위 더 높은 것 있으면 뒤로 보내기
        if(priorities[document[0]]<max){
            document.push_back(document[0]);
            document.erase(document.begin());
        }
        //2-3.그렇지 않으면 출력
        else{
            document.erase(document.begin());
            answer++;

            //2-5.max 우선순위 저장
            max = -1;
            for(int i=0; i<document.size(); i++){
                if(max<priorities[document[i]]){
                    max = priorities[document[i]];
                }
            }
        }
    }
    return answer;
}
```
<br/><br/>

## 4. 문제해결능력 UP! 되짚어보기
- vector에서 front()와 back() 적극사용 => 큐 개념 명확히 명시 가능

<br/><br/>

## 5. References
1) 공식 C++ References (<https://modoocode.com/241>)
<br/><br/>
