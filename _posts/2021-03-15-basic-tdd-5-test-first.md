---
layout: post
title:  "TDD 입문하기 - 테스트 주도 개발 기초: 테스트 우선 개발"
categories: tdd
---

## 테스트 우선 개발
- 운영 코드보다 테스트 코드를 먼저 작성하는 개발 절차는 코딩의 수단보다 목적에 집중하도록 도와줍니다.
- 테스트 우선 개발을 사용해 라이브러리를 만들며 이런 효과를 맛봅니다.

<br>

### 테스트 코드
- 가시적이고 구체적인 목표
- 자가검증
- 반복실행
- 클라이언트

<br>

### 운영 코드보다 테스트 코드를 먼저 작성
1. 명확하고 검증 가능한 목표를 설정한 후 목표를 달성
2. 프로세스가 코딩에 앞선 목표 설정을 강요
3. 프로그래머는 자신이 풀어야 할 문제를 구체적으로 이해해야함

<br>

### 테스트 우선 개발 작성
- 운영 코드보다 테스트 코드먼저 작성
- 테스트 코드 실패 후 운영 코드 수정

<br>

### Faker 설치
- 랜덤 데이터 테스트
- 테스트 코드가 임의의 문자열을 선택

{% highlight command%}
npm install --save-dev faker
{% endhighlight %}

<br>

## 참고
[Code 1-3: 테스트 우선 개발](https://github.com/LeeYoonSam/InitiateTDDHandsOn/commit/80c47fb2cb0e3a13cd514329e8e7bd9fed39ddb5)

[패스트 캠퍼스 - The RED: 이규원의 현실 세상의 TDD: 안정감을 주는 코드 작성 방법.](https://www.fastcampus.co.kr/dev_red_ygw)

[TDD HandsOn](https://github.com/gyuwon/TDDHandsOn)