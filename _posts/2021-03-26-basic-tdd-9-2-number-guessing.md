---
layout: post
title:  "TDD 입문하기 - 테스트 주도 개발 기초: 장난감 2"
categories: tdd
---

# Number Guessing
1 ~ 100 사이 정수를 추측해서 맞추는 콘솔 게임

## Parameterized Test
Junit 5 - 파라미터라이즈 테스트 지원

### Gradle Dependencies
```
testImplementation 'org.junit.jupiter:junit-jupiter-params:5.6.0'
```

### ParameterizedTest

**파라미터를 제공하는 수단**
<br>

@CsvSource

{% highlight java%}
@ParameterizedTest
@CsvSource({ "50, 40", "30, 20"})
void some_test(int first, int second)
{% endhighlight %}
- 따옴표(")로 테스트 파라미터 세트 지정
- 콤마(,) 로 각 파라미터 구분

<br>

@ValueSource

{% highlight java%}
@ParameterizedTest
@ValueSource(ints = { 1, 2, 3, 4, 5 })
void some_test(int answer)
{% endhighlight %}
- 파라미터가 하나인경우 사용

<br>

[<< 정리된 코드](./../17/basic-tdd-6-organized-code) [장난감 3 >>](./../29/basic-tdd-9-3-number-guessing) 

<br>

## 참고

| base | complete |
| [장난감-2 base](https://github.com/LeeYoonSam/InitiateTDDHandsOn/tree/%EC%9E%A5%EB%82%9C%EA%B0%90-2-base/NumberGuessing) | [장난감-2 complete](https://github.com/LeeYoonSam/InitiateTDDHandsOn/tree/%EC%9E%A5%EB%82%9C%EA%B0%90-2-complete/NumberGuessing) |

[패스트 캠퍼스 - The RED: 이규원의 현실 세상의 TDD: 안정감을 주는 코드 작성 방법.](https://www.fastcampus.co.kr/dev_red_ygw)

[TDD HandsOn](https://github.com/gyuwon/TDDHandsOn)