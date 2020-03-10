---
layout: post
title: "Programmers 코딩 테스트 고득점 Kit_ [정렬] K번째수"
date: 2020-03-08
categories: Programmers Sort C++
---

- 문제 유형: 정렬_자료를 일정한 규칙에 따라 나열하는 것
- 난이도: level_01 (약 13,529명 완료)
- 사용 언어: C++ <br/><br/>

## 1. 문제
### 1) K번째수
배열 array의 i번째 숫자부터 j번째 숫자까지 자르고 정렬했을 때, k번째에 있는 수를 구하려 합니다.<br/>
예를 들어 array가 [1, 5, 2, 6, 3, 7, 4], i = 2, j = 5, k = 3이라면<br/>
- array의 2번째부터 5번째까지 자르면 [5, 2, 6, 3]입니다.<br/>
- 1에서 나온 배열을 정렬하면 [2, 3, 5, 6]입니다.<br/>
- 2에서 나온 배열의 3번째 숫자는 5입니다.  

배열 array, [i, j, k]를 원소로 가진 2차원 배열 commands가 매개변수로 주어질 때, commands의 모든 원소에 대해 앞서 설명한 연산을 적용했을 때 나온 결과를 배열에 담아 return 하도록 solution 함수를 작성해주세요.
<br/>

### 2) 제한사항   
- array의 길이는 1 이상 100 이하입니다.
- array의 각 원소는 1 이상 100 이하입니다.
- commands의 길이는 1 이상 50 이하입니다.
- commands의 각 원소는 길이가 3입니다.

### 3) 기본코드
```c++
#include <string>
#include <vector>

using namespace std;

vector<int> solution(vector<int> array, vector<vector<int>> commands) {
    vector<int> answer;
    return answer;
}
```
<br/>

## 2. 알고리즘! 생각해보자
1) 배열 array의 i번째부터 j번째까지 잘라 sub_arr에 저장
- i==j인 경우, array[i] 번째 값 sub_arr에 저장
- 이외의 경우, i번째부터 j번째까지 복사해서 sub_arr에 저장  

2) sub_arr 정렬하기
- 단, "i==j인 경우"에는 sub_arr내의 원소가 한 개뿐이므로 정렬이 필요하지 않음

3) k번째 숫자 return
<br/><br/>

## 3. 해결코드
[C++]<br/>

```c++
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

vector<int> solution(vector<int> array, vector<vector<int>> commands) {
    vector<int> answer;

    int length;

    //1.배열 array의 i번째부터 j번째까지 잘라 sub_arr에 저장
    for(int i=0; i<commands.size(); i++){
        vector<int> sub_arr;

        //1-1.i==j인 경우, array[i] 번째 값 sub_arr에 저장
        if(commands[i][1] == commands[i][0]){
            sub_arr.push_back(array[commands[i][0]-1]);
        }
        //1-2.이외의 경우, i번째부터 j번째까지 복사해서 sub_arr에 저장
        else {
            length = commands[i][1]-commands[i][0]+1;
            sub_arr.resize(length);
            copy(array.begin()+commands[i][0]-1, array.begin()+commands[i][1], sub_arr.begin());

            //2.sub_arr 정렬
            sort(sub_arr.begin(), sub_arr.end());
        }

        //3. k번째 숫자 return
        answer.push_back(sub_arr[commands[i][2]-1]);
    }
    return answer;
}
```  
<br/>

## 4. 문제해결능력 UP! 되짚어보기
- vector 자료형 사용시, copy()와 assign() 차이점

  \- copy() : vector의 <u>"size"가 미리 할당되어야</u> 사용가능 <br/>
  \- assign() : size가 할당되어 있지 않아도 사용 가능 [(assign() 사용하여 문제 해결한 코드)](https://0pencoding.github.io/%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%A8%B8%EC%8A%A4%EA%B3%A0%EB%93%9D%EC%A0%90kit/level1/2020/03/03/%EC%A0%95%EB%A0%AC_K%EB%B2%88%EC%A7%B8%EC%88%98_level1.html)
<br/><br/>

## 5. References
1) copy(), assign() 사용법 (<https://blog.box.kr/?p=439>)<br/>
2) sort() 사용법 (<https://blockdmask.tistory.com/178>)<br/>
3) 공식 C++ References (<https://modoocode.com/241>)
<br/><br/>
