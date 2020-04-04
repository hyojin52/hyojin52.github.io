---
layout: post
title: "Programmers 코딩 테스트 고득점 Kit_ [해시] 베스트 앨범"
date: 2020-04-03
categories: Programmers Hash C++
---

- 문제 유형: 해시_Key-value쌍으로 데이터를 저장하는 자료구조
- 난이도: level_03 (약 4,235명 완료)
- 사용 언어: C++ <br/><br/>

## 1. 문제
### 1) 베스트 앨범
스트리밍 사이트에서 장르 별로 가장 많이 재생된 노래를 두 개씩 모아 베스트 앨범을 출시하려 합니다. 노래는 고유 번호로 구분하며, 노래를 수록하는 기준은 다음과 같습니다.<br/>

1. 속한 노래가 많이 재생된 장르를 먼저 수록합니다.
2. 장르 내에서 많이 재생된 노래를 먼저 수록합니다.
3. 장르 내에서 재생 횟수가 같은 노래 중에서는 고유 번호가 낮은 노래를 먼저 수록합니다.

노래의 장르를 나타내는 문자열 배열 genres와 노래별 재생 횟수를 나타내는 정수 배열 plays가 주어질 때, 베스트 앨범에 들어갈 노래의 고유 번호를 순서대로 return 하도록 solution 함수를 완성하세요.
<br/>

### 2) 제한사항   
- genres[i]는 고유번호가 i인 노래의 장르입니다.
- plays[i]는 고유번호가 i인 노래가 재생된 횟수입니다.
- genres와 plays의 길이는 같으며, 이는 1 이상 10,000 이하입니다.
- 장르 종류는 100개 미만입니다.
- 장르에 속한 곡이 하나라면, 하나의 곡만 선택합니다.
- 모든 장르는 재생된 횟수가 다릅니다.

### 3) 기본코드
```c++
#include <string>
#include <vector>

using namespace std;

vector<int> solution(vector<string> genres, vector<int> plays) {
    vector<int> answer;
    return answer;
}
```
<br/><br/>

## 2. 알고리즘! 생각해보자
문제 유형이 hash이고, "장르별 정렬, 재생횟수별 정렬"을 수행해야하므로 아래와 같은 자료구조의 필요성을 느낌<br/>
```
  장 르 |- 고유번호 - 재생횟수
        |- 고유번호 - 재생횟수
        |- 고유번호 - 재생횟수
    ''        ''         ''
    ''        ''         ''
    ''        ''         ''      =>  map<string, vector<pair<int, int>>> play_list;
```
하지만... C++에 대한 부족한 코딩실력으로 인해 결국 set과 multimap, vector 등 많은 자료구조를 이용하여 문제를 해결(너무 비효율적인 낭비가 많았던 코드라 반성해야 된다...ㅠ)

1) 장르별 정렬, 재생횟수별 정렬
2) 정렬된 순서에 따라 anwer완성
<br/><br/>

## 3. 해결코드
[C++]<br/>

```c++
#include <string>
#include <vector>
#include <map>
#include <set>
#include <algorithm>

using namespace std;

bool cmp1(const pair<int, string>& l, const pair<int, string>& r){
    return l.first>r.first;
}

bool cmp2(const pair<int, int>& l, const pair<int, int>& r){
    if(l.first == r.first) return l.second<r.second;
    return l.first>r.first;
}

vector<int> solution(vector<string> genres, vector<int> plays) {
    vector<int> answer;

    //1.각 변수 초기 설정
    set<string> gen;
    set<string>::iterator sit;
    multimap<string, int> gen_id;
    multimap<string, int>::iterator mit;
    for(int i=0; i<genres.size(); i++){
        gen.insert(genres[i]);
        gen_id.insert(make_pair(genres[i], i));
    }

    //2. 장르별 정렬, 재생횟수별 정렬
    vector<pair<int, string>> rank_gen;
    vector<pair<int, int>> rank_plays;
    int idx = 0;
    for(sit=gen.begin(); sit!=gen.end(); sit++){
        rank_gen.push_back(make_pair(0, *sit));
        for(mit = gen_id.lower_bound(*sit); mit != gen_id.upper_bound(*sit); mit++){
            (rank_gen.end()-1)->first += plays[mit->second];
            rank_plays.push_back(make_pair(plays[mit->second], mit->second));
        }
        sort(rank_plays.begin()+idx, rank_plays.begin()+idx+gen_id.count(*sit), cmp2);
        idx += gen_id.count(*sit);
    }
    sort(rank_gen.begin(), rank_gen.end(), cmp1);

    //3. 정렬된 순서에 따라 anwer완성
    string genre;
    for(auto& id:rank_gen){
        idx = 0;
        genre = genres[rank_plays.begin()->second];
        while(id.second != genre){
            idx += gen_id.count(genre);
            genre = genres[(rank_plays.begin()+idx)->second];
        }

        if(gen_id.count(id.second) == 1)
            answer.push_back((rank_plays.begin()+idx)->second);
        else{
            for(int i=0; i<2; i++)
                answer.push_back((rank_plays.begin()+idx+i)->second);
        }         
    }

    return answer;
}
```
<br/><br/>

## 4. 문제해결능력 UP! 되짚어보기
- 다른 사람들 코드보고 반성하기...
<br/><br/>

## 5. References
1) [sort 함수 커스텀](https://withhamit.tistory.com/195)<br/>
2) [컨테이너 종류 및 hash_map](https://gamdekong.tistory.com/73)<br/>
2) [공식 C++ References](<https://modoocode.com/241>)
<br/><br/>

<div style="display:none">
//배워야 할 코드 1
#include <string>
#include <vector>
#include <unordered_map>
#include <algorithm>
#include <utility>

using namespace std;
bool compare (pair<int, int> left, pair<int, int> right){
    if(left.first > right.first){
        return true;
    }else if(left.first == right.first){
        if(left.second < right.second){
            return true;
        }
    }
    return false;
}

vector<int> solution(vector<string> genres, vector<int> plays) {
    vector<int> answer;
    unordered_map<string, int> summap;
    unordered_map<string, vector<pair<int, int>>> genmap;
    for (int i = 0; i < genres.size(); i++) {
        summap[genres[i]] += plays[i]; //어메이징
        genmap[genres[i]].push_back(make_pair(plays[i], i));
    }

    vector<pair<int, string>> fororder;
    for (auto x : summap) {
        fororder.push_back(make_pair(x.second, x.first));
    }
    sort(fororder.begin(), fororder.end());
    while (fororder.size() > 0) {
        pair<int, string> temp= fororder.back();
        fororder.pop_back();
        vector<pair<int, int>> a = genmap[temp.second];
        sort(a.begin(), a.end(), compare);
        answer.push_back(a[0].second);
        if (a.size() < 1)
            answer.push_back(a[1].second);
    }

    return answer;
}

//배워야 할 코드 2
#include <algorithm>
#include <vector>
#include <map>

using namespace std;

bool CompareGenere(pair<string, int> A, pair<string, int> B){
    return A.second > B.second;
}

bool ComparePlay(pair<int, int> A, pair<int, int> B){
    if(A.second == B.second)
        return A.first < B.first;
    return A.second > B.second;
}

vector<int> solution(vector<string> genres, vector<int> plays) {
    vector<int> answer;
    map<string, int> sums;
    map<string, vector<pair<int, int>>> play_list;

    for(int i = 0; i < plays.size(); ++i){
        sums[genres[i]] += plays[i];
        play_list[genres[i]].push_back(make_pair(i, plays[i]));
    }

    vector<pair<string, int>> sum_of_plays(sums.begin(), sums.end());
    sort(sum_of_plays.begin(), sum_of_plays.end(), CompareGenere);
    for(auto genere : sum_of_plays){
        sort(play_list[genere.first].begin(), play_list[genere.first].end(), ComparePlay);
        answer.push_back(play_list[genere.first][0].first);
        if(play_list[genere.first].size() > 1)
            answer.push_back(play_list[genere.first][1].first);
    }

    return answer;
}
</div>
