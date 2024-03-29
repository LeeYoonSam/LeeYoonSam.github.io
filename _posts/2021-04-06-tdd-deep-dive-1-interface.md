---
layout: post
title:  "TDD 입문하기 - 테스트 주도 개발의 깊은곳: 인터페이스와 구현"
categories: tdd
---


## 인터페이스와 구현
인터페이스와 구현은 코드를 구성하는 중요한 요소다.

두 요소의 역할을 떠올리고 설계 접근법을 소개

실무에서 TDD 와 자주 쓰일수 있는 기법, 기술, 도구 소개

<br><br>

### 추상화
- 주어진 맥락에 관련된 정보들을 남기고 동시에 주어진 맥락과 관련없는 정보를 잊어버리는 과정
- 목적에 따라 대상이 가진 특징의 일부만 투영하는 것
- 추상화 과정을 통해서 투영된 결과로 모델을 얻는다.

<br><br>

### 협력과 계약
- 대부분의 코드는 다른 코드와 협력
- 협력에 필요한 것은 '어떻게'가 아닌 '무엇'

<br><br>

### 인터페이스
- '무엇'을 표현
- 클라이언트 코드에게 반드시 필요한 정보
- 협력하는 코드 사이의 계약
- 추상화 결과

<br><br>

### 인터페이스에 프로그래밍
- 우리는 인터페이스를 대상으로 프로그래밍을 한다.
- 어떤것에 내용을 고려하지 않고 그것에 대해 프로그래밍을 한다.

<br><br>

### 구현
- 구현에 따라 다르게 작동
- 다른 구현을 제공

<br><br>

### 정보숨김

#### 효과적인 모듈화
- 조직 간 의사소통 최소화
- 변경 여파 최소화
- 시스템 이해 도움

<br>

#### 공개된 설계 결정과 숨겨진 설계 결정
- 어려운 설계 결정과 변경될 것 같은 설계 결정을 숨겨라.
- 대부분의 시스템 정보는 대부분의 프로그래머에게 숨겨지는 것이 도움이 된다.
- 대신 어려운 설계 결정이나 변경 될 가능성이 있는 설계 결정은 목록으로 시작하는 것이 좋다. 그런 다음 각 모듈은 이러한 결정을 다른 모듈로부터 숨기도록 설계된다.

<br><br>

[<< 장난감 3](./../../03/29/basic-tdd-9-3-number-guessing)

<br>

### 참고

[패스트 캠퍼스 - The RED: 이규원의 현실 세상의 TDD: 안정감을 주는 코드 작성 방법.](https://www.fastcampus.co.kr/dev_red_ygw)

[TDD HandsOn](https://github.com/gyuwon/TDDHandsOn)