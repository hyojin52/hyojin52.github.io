---
layout: post
title: "Programmers 코딩 테스트 고득점 Kit_ [완전탐색] 타겟넘버"
date: 2020-03-11
categories: Programmers DFS-BFS C++
---

- 문제 유형: DFS/BFS_깊이/넓이 우선으로 탐색하는 알고리즘
- 난이도: level_02 (약 4,868명 완료)
- 사용 언어: C++ <br/><br/>

## 1. 문제
### 1) 타겟넘버   
n개의 음이 아닌 정수가 있습니다. 이 수를 적절히 더하거나 빼서 타겟 넘버를 만들려고 합니다. 예를 들어 [1, 1, 1, 1, 1]로 숫자 3을 만들려면 다음 다섯 방법을 쓸 수 있습니다.<br/>
```
-1+1+1+1+1 = 3
+1-1+1+1+1 = 3
+1+1-1+1+1 = 3
+1+1+1-1+1 = 3
+1+1+1+1-1 = 3
```
사용할 수 있는 숫자가 담긴 배열 numbers, 타겟 넘버 target이 매개변수로 주어질 때 숫자를 적절히 더하고 빼서 타겟 넘버를 만드는 방법의 수를 return 하도록 solution 함수를 작성해주세요.
<br/>

### 2) 제한사항   
- 주어지는 숫자의 개수는 2개 이상 20개 이하입니다.
- 각 숫자는 1 이상 50 이하인 자연수입니다.
- 타겟 넘버는 1 이상 1000 이하인 자연수입니다.

### 3) 기본코드
```c++
#include <string>
#include <vector>

using namespace std;

int solution(vector<int> numbers, int target) {
    int answer = 0;
    return answer;
}
```
<br/><br/>

## 2. 알고리즘! 생각해보자
1) 접근방법
```
answer++ <- target==() <- d+(c+(a+b)) <- c+(a+b) <- a+b
그렇다면............... ================================: 계속 반복되는 부분
<--------base---------><||||||||||recursive|||||||||||>
```
<br/><br/>

## 3. 해결코드
[C++]<br/>

```c++
#include <string>
#include <vector>
#include <map>

using namespace std;

int recursive(vector<int> arr, int goal, int sum){
    int temp;

    if(arr.size() == 0){
        if(goal == sum){
            return 1;
        }
        else{
            return 0;
        }
    }
    else{
        temp = arr[0];
        arr.erase(arr.begin());
        return recursive(arr, goal, sum+temp)+recursive(arr, goal, sum-temp);
    }
}

int solution(vector<int> numbers, int target) {
    int answer = 0;

    answer = recursive(numbers, target, 0);

    return answer;
}
```
<br/><br/>

## 4. 문제해결능력 UP! 되짚어보기
- DFS(재귀함수, stack 주로 이용), BFS(queue 주로 이용)
- 재귀함수 느낌 코드로 나타낼 수 있으려면 어떻게 해야할까... ^^;
<br/><br/>

## 5. References
1) DFS 및 BFS 개념 (<https://twpower.github.io/151-bfs-dfs-basic-problem>)<br/>
2) recursive 개념 및 예제 (<https://excelsior-cjh.tistory.com/28>)<br/>
3) 공식 C++ References (<https://modoocode.com/241>)
<br/><br/>
