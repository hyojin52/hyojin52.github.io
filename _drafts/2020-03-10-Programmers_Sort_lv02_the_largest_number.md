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
1)
<br/><br/>

## 3. 해결코드
[C++]<br/>

```c++
#include <string>
#include <vector>
#include <stack>
#include <algorithm>

using namespace std;

string solution(vector<int> numbers) {
    string answer = "";

    //1.각 자리수별(1, 10, 100, 1000) stack 생성
    vector<int> one, two, three, four;

    for(int i=0; i<numbers.size(); i++){
        if(numbers[i]/1000 > 0 && numbers[i]/1000 < 10)
            four.push_back(numbers[i]);
        else if(numbers[i]/100 > 0 && numbers[i]/100 < 10)
            three.push_back(numbers[i]);
        else if(numbers[i]/10 > 0 && numbers[i]/10 < 10)
            two.push_back(numbers[i]);
        else
            one.push_back(numbers[i]);
    }

    if(one.size()!=0) sort(one.begin(), one.end());
    if(two.size()!=0) sort(two.begin(), two.end());
    if(three.size()!=0) sort(three.begin(), three.end());
    if(four.size()!=0) sort(four.begin(), four.end());   

    //2. 각 스택에서 하나씩 pop해서 temp에 넣고 크기 비교 뒤, 숫자 생성하기
    vector<int> temp;
    for(int i=0; i<numbers.size(); i++){
        if(one.size()!=0) temp[0] = one[one.size()-1];
        else temp[0] = 0;

        if(two.size()!=0) temp[1] = two[two.size()-1];
        else temp[1] = 0;

        if(three.size()!=0) temp[2] = three[three.size()-1];
        else temp[2] = 0;

        if(four.size()!=0) temp[3] = four[four.size()-1];
        else temp[3] = 0;
    }

    return answer;
}
```  
<br/>

## 4. 문제해결능력 UP! 되짚어보기
-

<br/><br/>

## 5. References
1) 공식 C++ References (<https://modoocode.com/241>)
<br/><br/>
