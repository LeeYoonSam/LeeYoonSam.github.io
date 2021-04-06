---
layout: post
title:  "TDD 입문하기 - 테스트 주도 개발 기초: 장난감 3"
categories: tdd
---

# Number Guessing
1 ~ 100 사이 정수를 추측해서 맞추는 콘솔 게임

<br>

## TDD 로 개발
> Red -> Green -> Refactor 의 반복

- 테스트 해야 할 부분을 생각하고 이것을 테스트 코드로 먼저 작성
- 테스트 코드 실패(Red) > 운영코드 작성
- 테스트를 통과하도록 운영코드 작성(Green) > 실패시 운영코드 계속 수정
- 중복되거나 지저분한 코드들을 분리 가능하다면 수정(Refactor)
- 리팩토링 및 운영코드 작성을 하면서 계속해서 모든 테스트코드가 잘 통과 하는지 확인하며 진행

<br>

### 어려운 부분
- 테스트 작성을 할때 어떤것을 어떻게 테스트 코드로 작성해야 하는지 선정하기 어려움.

<br>

## 인수 테스트
> 개발이 완료 되고 실제로 실행해보며 전체 수동 테스트를 진행하는 것.

- 유닛 테스트가 통과했음에도 불구하고 변경해야 하는 일이 발생
- 간단한 수정이라도 관련된 테스트 코드가 있으면 해당 테스트를 수정하고 리팩토링
- 완전 새로운 문제라면 테스트 코드를 추가로 작성하고 운영코드 리팩토링
- 인수 테스트를 다시 실행할때도 처음부터 다시 테스트

<br>
<br>

[<< 장난감 2](./../26/basic-tdd-9-2-number-guessing)  [인터페이스와 구현 >>](./../../04/06/tdd-deep-dive-1-interface)

<br>

## 참고

| base | complete |
| [장난감-3 base](https://github.com/LeeYoonSam/InitiateTDDHandsOn/tree/%EC%9E%A5%EB%82%9C%EA%B0%90-2-complete/NumberGuessing) | [장난감-3 complete](https://github.com/LeeYoonSam/InitiateTDDHandsOn/tree/%EC%9E%A5%EB%82%9C%EA%B0%90-3-complete/NumberGuessing) |

[패스트 캠퍼스 - The RED: 이규원의 현실 세상의 TDD: 안정감을 주는 코드 작성 방법.](https://www.fastcampus.co.kr/dev_red_ygw)

[TDD HandsOn](https://github.com/gyuwon/TDDHandsOn)