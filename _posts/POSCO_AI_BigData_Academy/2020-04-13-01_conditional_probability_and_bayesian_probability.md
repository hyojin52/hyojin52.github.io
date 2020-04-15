---
layout: post
title: "확률및통계_01. 조건부확률과 베이지안이론"
date: 2020-04-06
categories: POSCO AI BigData YABA Probability Statistics
---

[확률 및 통계](https://www.youtube.com/watch?v=2ewO_6msPbA&list=PLSN_PltQeOyjmRIsC7VNirXOBqWoypd4V&index=2&t=0s)는 Youtube에서 시청가능합니다.<br/><br/>

## 1. 조건부확률
---
먼저 조건부확률의 개념을 그림으로 표현하면 아래와 같다.<br/>
<img src="https://lh3.googleusercontent.com/proxy/pRdlgV9dbSHNE9MnAVHYu_I_qFOXYebWPxo-tSEaRrQP5NjRwn9mbfLpOeDtrbDJN6IfKZhpuGTzfp9nHJa62KTuxxS1xjfbgTXaqwRwbgnXN0q2n1ORwBTzMbR1rujNM_LrNUxW2buH-3H6YOz9wXW_uVHhXEbDia-sDrlY_f7HTepyGHpp86zT7uqWwZdGwCl8_A">

또한 식으로 조건부확률의 개념을 이해해본다면...<br/>
P(A) = P(A1)+P(A2)+...+P(An) ⇒ A1,2,...n 은 partition of A<br/>
P(A1) = P(A1 교 A) = P(A|A1)P(A1)<br/>
P(An) = P(An 교 A) = P(A|An)P(An)<br/>
따라서, P(A) = sum{ P(A|An)P(An) }
<br/><br/>

## 2. Bayesian Theorem
---
1) P(B\|A) = P(B 교 A)/P(A) = P(A\|B)P(B)/P(A)<br/>
:: P(B\|A)를 구하고 싶은데 구할 수 없을 때 P(A\|B)를 알고있다면, P(A\|B)를 이용해서 P(B\|A) 구하기<br/>

2) P(Ai\|A) = P(A\|Ai)P(Ai)/P(A)
  - 이때, Ai = unknown original input, A = observation data,

(ex_1.7) Binary Symmetric Channel<br/>
- X(송신자)가 1을 보내면 Y(수신자)가 1을 받을 확률 =  P11
  - P11=P22, P12=P21 이면, Binary Symmetric 통신환경이라고 한다.

- Symmetric 통신환경은 베이지안 이론에 해당하므로, Pn = P(y1\|x1)
  - y1: observation data 1(수신자가 받은 값)
  - x1: original input 1(송신자가 보낸 값)

- P error = P(x1 transmit, y2 receive)+P(x2 transmit, y1 receive) = P(y2\|x1)P(x1)+P(y1\|x2)P(x2)

- y2를 받았을때, x1으로부터 전송받았을 확률?
  - P(x1\|y2) : x1_input data 1, y2_observation data 2<br/>
  - 베이지안 이론 활용하여 P(x1\|y2) = P(y2\|x1)P(x1)/{ P(y2) } = P(y2\|x1)P(x1)/{ P(y2\|x1)P(x1)+P(y2\|x2)P(x2) }<br/>

- P(x1\|error)?
  - P(y2\|x1)P(x1)/P(y2\|x1)P(x1)+P(y1\|x2)P(x2)
<br/><br/>

## 3. Independent Events(독립사건)
---
- P(A\|B) = P(A)
- P(B\|A) = P(B) = P(A 교 B)/P(A) ⇒ P(A 교 B) = P(A)P(B)
- independent ≠ exclusive
- A,B 가 독립이라면, A와 not B, not A와 B, not A와 not B도 독립

<br/><br/>
## 4. Conbined Experiments
---
- 두 사건 S1, S2에 대해서 S=S1*S2(\*: cartesion product) = {(s1, s2), (a1, b2), ... }

(ex_1) 3 coin tossing<br/>
S1 = {앞, 뒤}<br/>
S2 = {앞, 뒤}<br/>
S3 = {앞, 뒤}<br/>
⇒ S = {(S1, S2, S3)| (앞, 앞, 앞), (앞, 앞, 뒤), ... )}, n(S) = 8
<br/><br/>

## References
---
- [확률 및 통계](https://www.youtube.com/watch?v=2ewO_6msPbA&list=PLSN_PltQeOyjmRIsC7VNirXOBqWoypd4V&index=2&t=0s)

<br/><br/>
