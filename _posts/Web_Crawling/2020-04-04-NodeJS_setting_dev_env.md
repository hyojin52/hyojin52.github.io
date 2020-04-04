---
layout: post
title: "Web Crawling: 1.개발환경 설정"
date: 2020-04-04
categories: Web-Crawling NodeJS VM CentOS
toc: true
---
- 목표: 가상머신 위에 개발 환경 구축하기
- 주요도구 및 라이브러리: VirtualBox/Vagrant, CentOS, Node.js, nvm, git

<span class="evidence">"글 내용 중에 미흡한 부분이 있을 수 있습니다. ^^ 댓글로 남겨주세요!"</span><br/>

yes24에서 열정적으로 책을 골라 구매한 뒤... 책장에 고이 모셔두었던 "자바스크립트와 Node.js를 이용한 웹 크롤링 테크닉(쿠지라 히코우즈쿠에 지음/이동규 옮김)"를 기초로 해서 웹 크롤링을 통한 데이터 수집-저장-분석에 대한 공부를 이어나가보려한다.<br/>

우선 본격적으로 프로젝트를 진행하기 전에 "개발환경 설정"부터 진행해보자!<br/><br/>

## 1. 가상머신 생성
### 1) VirtualBox와 Vagrant 설치
다음의 링크를 활용하여 컴퓨터의 운영체제에 맞는 [VirtualBox](https://www.virtualbox.org/wiki/Downloads)와 [Vagrant](https://www.vagrantup.com/downloads.html)를 다운로드한다.<br/>
- Vagrant란? 가상머신의 환경 및 권한설정 도구(provisioning)
<br/>

### 2) 가상머신 추가
가상머신 생성을 위해 ``` vagrant init ``` 명령어를 사용한다. CentOS 설치를 위해 생성된 Vagrantfile에 아래와 같이 코드를 수정한다.

```
#config.vm.box = "base" 주석처리
config.vm.box = "puphpet/centos65-x64" #추가
```

### 3) Vagrant 기본 사용을 위한 명령어
<table border='1' bordercolor='black' width ='60%'>
  <tr style="background-color:#e3e3e3">
    <th>명령어</th>
    <th>설명</th>
  </tr>
  <tr>
    <td align ="center">vagrant up</td>
    <td align ="center">가상머신 On</td>
  </tr>
  <tr>
    <td align ="center">vagrant halt</td>
    <td align ="center">가상머신 Off</td>
  </tr>
  <tr>
    <td align ="center">vagrant reload</td>
    <td align ="center">가상머신 Re-On</td>
  </tr>
  <tr>
    <td align ="center">vagrant suspend</td>
    <td align ="center">가상머신 정지</td>
  </tr>
  <tr>
    <td align ="center">vagrant resume</td>
    <td align ="center">가상머신 정지에서 복원</td>
  </tr>
  <tr>
    <td align ="center">vagrant status</td>
    <td align ="center">가상머신 상태 확인</td>
  </tr>
  <tr>
    <td align ="center">vagrant destroy</td>
    <td align ="center">가상머신 삭제</td>
  </tr>
  <tr>
    <td align ="center">vagrant ssh</td>
    <td align ="center">가상머신 로그인</td>
  </tr>
</table>
<br/><br/>

# 2.Node.JS 설치
다음 포스트([Node.js 설치방법](https://blog.stories.pe.kr/225))에서 친절한 설명과 함께 다루고 있다.
- Node.js란? 자바스크립트의 엔진
- npm이란? 노드(Node.js)의 패키지/모듈 관리자
- nvm이란? 노드(Node.js)의 버전 관리자

다음 글에서는 본격적으로 Node.js를 활용한 웹 데이터 수집을 진행할 것이다.<br/>
<br/><br/>

## 3. References
1) [도서_자바스크립트와 Node.js를 이용한 웹 크롤링 테크닉](http://www.yes24.com/Product/Goods/34907983?scode=032&OzSrank=1)
2) [Node.js설치 및 환경설정](https://blog.stories.pe.kr/225)
<br/><br/>
