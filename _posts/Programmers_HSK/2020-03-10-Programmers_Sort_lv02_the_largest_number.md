---
layout: post
title: "Programmers 코딩 테스트 고득점 Kit_ [정렬] 가장 큰 수"
date: 2020-03-08
categories: Programmers Sort C++
---

- 문제 유형: 정렬_자료를 일정한 규칙에 따라 나열하는 것
- 난이도: level_02 (약 4,761명 완료)
- 사용 언어: C++ <br/><br/>

## 1. 문제
### 1) 가장 큰 수
0 또는 양의 정수가 주어졌을 때, 정수를 이어 붙여 만들 수 있는 가장 큰 수를 알아내 주세요.<br/>

예를 들어, 주어진 정수가 [6, 10, 2]라면 [6102, 6210, 1062, 1026, 2610, 2106]를 만들 수 있고, 이중 가장 큰 수는 6210입니다.<br/>

0 또는 양의 정수가 담긴 배열 numbers가 매개변수로 주어질 때, 순서를 재배치하여 만들 수 있는 가장 큰 수를 문자열로 바꾸어 return 하도록 solution 함수를 작성해주세요.
<br/>   

### 2) 제한사항   
- numbers의 길이는 1 이상 100,000 이하입니다.
- numbers의 원소는 0 이상 1,000 이하입니다.
- 정답이 너무 클 수 있으니 문자열로 바꾸어 return 합니다.  

### 3) 기본코드
```c++
#include <string>
#include <vector>

using namespace std;

string solution(vector<int> numbers) {
    string answer = "";
    return answer;
}
```
<br/><br/>

## 2. 알고리즘! 생각해보자
1) sort 함수에서 비교함수 customizing해서 정렬<br/>
2) 가장 큰 수 만들어주기<br/>
3) numbers의 값이 "모두 0"인 경우 예외처리
<br/><br/>

## 3. 해결코드
[C++]<br/>

```c++
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

bool compare(int num1, int num2){
    string temp1, temp2;

    temp1 = to_string(num1);
    temp2 = to_string(num2);

    return temp1+temp2 > temp2+temp1;
}

string solution(vector<int> numbers) {
    string answer = "";

    //1.numbers에 들어있는 값들 sort(비교함수 사용해서)
    sort(numbers.begin(), numbers.end(), compare);

    //2.가장 큰 숫자 만들어주기
    for(int i=0; i<numbers.size(); i++){
        answer.append(to_string(numbers[i]));
    }

    //3. 모두 0인 예외 case 처리
    if(answer[0] == '0') answer = '0';

    return answer;
}
```  
<br/>

## 4. 문제해결능력 UP! 되짚어보기
- sort()의 compare하는 함수도 직접 변경 가능하다!!
- 모두 해결했다고 생각했지만 끝이 아닐수도... 예외 case 생각하기

<br/><br/>

## 5. References
1)  sort 함수 활용한 정렬 (<https://twpower.github.io/71-use-sort-and-stable_sort-in-cpp>)<br/>
2) 공식 C++ References (<https://modoocode.com/241>)
<br/><br/>
