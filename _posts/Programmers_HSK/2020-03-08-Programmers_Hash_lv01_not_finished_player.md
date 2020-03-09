---
layout: post
title: "Programmers 코딩 테스트 고득점 Kit_ [해시] 완주하지 못한 선수"
date: 2020-03-08
categories: Programmers Hash C++
---

- 문제 유형: 해시_Key-value쌍으로 데이터를 저장하는 자료구조
- 난이도: level_01 (약 15,702명 완료)
- 사용 언어: C++ <br/><br/>

## 1. 문제
### 1) 완주하지 못한 선수   

수많은 마라톤 선수들이 마라톤에 참여하였습니다. 단 한 명의 선수를 제외하고는 모든 선수가 마라톤을 완주하였습니다. 마라톤에 참여한 선수들의 이름이 담긴 배열 participant와 완주한 선수들의 이름이 담긴 배열 completion이 주어질 때, 완주하지 못한 선수의 이름을 return 하도록 solution 함수를 작성해주세요.<br/>

### 2) 제한사항   

- 마라톤 경기에 참여한 선수의 수는 1명 이상 100,000명 이하입니다.<br/>
- 길이는 participant의 길이보다 1 작습니다.<br/>
- 참가자의 이름은 1개 이상 20개 이하의 알파벳 소문자로 이루어져 있습니다.<br/>
- 참가자 중에는 동명이인이 있을 수 있습니다.<br/>  

### 3) 기본코드
```c++
#include <string>
#include <vector>

using namespace std;

string solution(vector<string> participant, vector<string> completion) {
    string answer = "";
    return answer;
}
```
<br/>

## 2. 알고리즘! 생각해보자
1) participant와 completion에 담긴 이름을 모두 비교한다. (반복문)
   - participant와 completion에 모두 이름이 있다면, 해당 이름을 participant와 completion에서 삭제한다.
   - 그렇지 않다면, 반복문 continue

2) participant에 남아있는 이름을 answer에 추가하여 return
<br/><br/>

## 3. 해결코드
[C++]<br/>

1) 초반코드(정확성_통과, 효율성_실패)
```c++
#include <string>
#include <vector>
#include <iostream>

using namespace std;

string solution(vector<string> participant, vector<string> completion) {
    string answer = "";

    int p_id = 0;
    int c_id = 0;

    for(p_id=0; p_id<participant.size(); p_id++){
        for(c_id=0; c_id<completion.size(); c_id++){
            if(participant[p_id].compare(completion[c_id]) == 0){
                participant[p_id] = "";
                completion[c_id] = "";
                break;
            }
        }        
    }

    for(p_id=0;p_id<participant.size();p_id++){
        if(participant[p_id].compare("") != 0 ){
            answer.assign(participant[p_id]);
            break;
        }
    }

    return answer;
}
```
아래와 같은 **문제점** 이 있음을 발견했다.<br/>
- 문제의 주제인 <u>해시</u> 개념 미사용
- 다중 반복문 사용으로 <u>효율성</u>이 떨어짐

문제점을 보완하여 다음과 같이 map 자료형을 이용하여 수정해보았다.<br/>

2) 수정코드(정확성_통과, 효율성_통과)
```c++
#include <string>
#include <vector>
#include <map>

using namespace std;

string solution(vector<string> participant, vector<string> completion) {
    string answer = "";

    map<string, int> temp;

    //1.map 초기화
    for(int i=0; i<participant.size(); i++){
        //1-1.key = participant에 담긴 이름, value = participant에 담긴 이름의 횟수
        if(temp.count(participant[i])==0)
            temp.insert(pair<string, int>(participant[i], 1));
        else
            (temp.find(participant[i])->second)++;
    }

    //2.tmep와 completion 비교
    for(int i=0; i<completion.size(); i++){
        //2-1.completion 명단에 있다면 횟수 줄이기
        (temp.find(completion[i])->second)--;
    }

    //3. temp 확인하여 answer 도출
    for(int i=0; i<participant.size(); i++){
        if(temp.find(participant[i])->second >= 1)
            answer = participant[i];
    }

    return answer;
}
```  
<br/>

## 4. 문제해결능력 UP! 되짚어보기
- 효율성을 높일 수 있도록 문제에 알맞은 자료형 선택하기
- map, set, unordered_map, unordered_set의 차이점
- 다양한 풀이법(정렬&비교 방법, multiset 자료형 이용 등)
<br/><br/>

## 5. References
1) vector 사용법 (<https://blockdmask.tistory.com/70>)<br/>
2) map 사용법 (<https://blockdmask.tistory.com/87>)<br/>
3) 공식 C++ References (<https://modoocode.com/241>)
<br/><br/>
