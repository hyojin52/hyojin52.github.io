---
layout: post
title: "Web Crawling: 2-1.웹 페이지 다운로드"
date: 2020-04-05
categories: Web-Crawling NodeJS
toc: true
---

- 목표: 웹 페이지 다운로드
- 주요도구 및 라이브러리: Node.js, Rhino, Nashorn

-------------------------------------------------------------------------------------------------------------
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#8251; 해당 포스트는 "자바스크립트와 Node.js를 이용한 웹 크롤링 테크닉" 도서를 기반으로 하고 있습니다. <br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 문제가 될 경우 삭제하도록 하겠습니다.<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#8251; 글 내용 중에 미흡한 부분이 있을 수 있습니다. ^^ 댓글로 남겨주세요!<br/>

-------------------------------------------------------------------------------------------------------------

<br/>
프로젝트 시작을 알리는 첫번째 챕터! Node.js를 활용하여 웹 페이지를 다운로드 해보자. 아래의 코드는 [JPub Github](https://github.com/Jpub/JSWebCrawler)에서 다운로드 가능하다.<br/><br/>

## 1. 웹 페이지 다운로드(Node.js)
-------------------------------------------------------------------------------------------------------------
### 1) 기본코드
``` javascript
// url 에 있는 파일을 savepath 에 다운로드한다
// 다운로드할 URL을 지정
// var url = "http://www.naver.com/";
var url = "http://hisnet.handong.edu/";

// 저장할 위치를 지정
var savepath = "test.html";

// 사용 모듈 정의 ---- (※ 1)
var http = require('http'); // HTTP 모듈
var fs = require('fs'); // 파일처리 관련 모듈

// 출력 지정 --- (※ 2)
var outfile = fs.createWriteStream(savepath);

// 비동기로 URL의 파일 다운로드 --- (※ 3)
http.get(url, function(res) {
    res.pipe(outfile); // --- (※ 4)
    res.on('end', function () { // --- (※ 5)
        outfile.close();
        console.log("ok");
    });
});
```
위의 코드를 실행하면 test.html 파일이 생성된다. url 변수에 [Naver 주소](http://www.naver.com/)를 입력한 경우, test.html 파일에서 302 Found 결과를 얻을 수 있었다. 302는 Redirect로, 요청한 리소스가 임시적으로 새로운 URL로 이동했음(Temporarily Moved)을 나타낸다. 해당 주소는 http이고, 현재 Naver 홈페이지는 https이기 때문에 302 Found와 같은 결과를 얻은 것 같다.<br/>

다음으로 url 변수에 [한동대학교 주소](http://hisnet.handong.edu/)를 입력한 경우, 아래와 같은 test.html 파일을 생성하였다.

![result](/assets/img/web_crawling/02-01-result.PNG)
<br/>

### 2) 함수화한 코드
위의 기본코드를 함수화하여 리팩토링한 코드이다.
``` javascript
// 다운로드
download(
  "http://jpub.tistory.com/539",
  "spring.html",
  function(){ console.log("ok, spring."); });

download(
  "http://jpub.tistory.com/537",
  "angular.html",
  function(){ console.log("ok, angular."); });

// url 의 파일을 savepath 에 다운로드하는 함수
function download(url, savepath, callback) {
  var http = require('http');
  var fs = require('fs');
  var outfile = fs.createWriteStream(savepath);

  var req = http.get(url, function(res) {
    res.pipe(outfile);
    res.on('end', function () {
      outfile.close();
      callback();
    });
  });
}
```
<br/><br/>

# 2.웹 페이지 다운로드(Rhino/Narshon)
-------------------------------------------------------------------------------------------------------------
Rhino와 Narshon의 경우 "자바"를 기반으로하고 있는 자바스크립트 엔진으로 Node.js와 비교했을 때 자바 API를 사용할 수 있다는 강력한 장점이 존재한다. 아래 코드는 위의 Node.js를 활용한 웹 페이지 다운로드와 동일한 동작을 하는 코드이다.<br/>
다만, 해당 코드를 실행하기 위해서는 Rhino와 Narshon을 설치하는 과정이 요구된다.<br/>

### 1) 기본코드
``` java
// url 에 있는 파일을 savepath 에 다운로드한다
var url = "http://jpub.tistory.com/";
var savepath = "test.html";

// 다운로드
var aUrl = new java.net.URL(url);
var conn = aUrl.openConnection(); // URL 에 접속 --- ( ※ 1)
var ins = conn.getInputStream(); // 입력스트림을 획득
var file = new java.io.File(savepath); 출력스트림을 획득 ---( ※ 2)
var out = new java.io.FileOutputStream(file);

// 입력스트림을 읽으면서 출력 스트림에 쓴다---- ( ※ 3)
var b;
while ((b = ins.read()) != -1) {
    out.write(b);
}
out.close(); // 출력 스트림을 닫는다. --- ( ※ 4)
ins.close(); // 입력 스트림을 닫는다.
```

### 2) 함수화한 코드
``` java
// 다운로드
download(
  "http://jpub.tistory.com/539",
  "spring.html");

download(
  "http://jpub.tistory.com/537",
  "angular.html");

print("ok");

// url 의 파일을 savepath 에 다운로드하는 함수
function download(url, savepath) {
  var aUrl = new java.net.URL(url);
  try {
    var conn = aUrl.openConnection();
    var ins = conn.getInputStream();
    var file = new java.io.File(savepath);
    var out = new java.io.FileOutputStream(file);
    var b;
    while ((b = ins.read()) != -1) {
      out.write(b);
    }
    out.close(); // 출력 스트림을 닫는다.
    ins.close(); // 입력 스트림을 닫는다.
  } catch (e) {
    throw new Error(e);
  }
}
```
<br/>

## 3. References
-------------------------------------------------------------------------------------------------------------
1) [도서_자바스크립트와 Node.js를 이용한 웹 크롤링 테크닉](http://www.yes24.com/Product/Goods/34907983?scode=032&OzSrank=1)<br/>
2) [예제 코드_JPub Github](https://github.com/Jpub/JSWebCrawler)
<br/><br/>
