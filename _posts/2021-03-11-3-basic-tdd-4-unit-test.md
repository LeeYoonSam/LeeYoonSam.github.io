---
layout: post
title:  "TDD 입문하기 - 테스트 주도 개발 기초: 단위 테스트"
categories: tdd
---

## 단위 테스트
- 단위 테스트는 테스트 주도 개발의 가장 중요한 도구 입니다.
- 기존 코도의 동작을 검증하는 단위 테스트를 작성해 봅니다.
- 전체 시스템 중 일부 코드에 대해 자동화를 하는 기법

<br>

### 단위 테스트 작성 대상 코드
- 문자열을 입력 받고 가공하는 함수
- 공백 문자가 있을경우 없애주는 기능을 하는 함수

제공되는 함수(자바 스크립트 코드)
{% highlight javascript %}
function refineText(s) {
    return s.replace("    ", " ").replace("  ", " ");
}

module.exports = refineText;
{% endhighlight %}

<br>

### 자바스크립트 테스트 도구인 Jest 설치
{% highlight terminal %}
npm install --save-dev jest
{% endhighlight %}

<br>

### 자바스크립트 테스트 코드 작성
- index.test.js 파일 생성
- sut(System under test): 테스트 대상 시스템

{% highlight javascript %}

const sut = require("./index");

test('sut transforms "hello  world" to "hello world"', () => {
    const actual = sut("hello  world");
    expect(actual).toBe("hello world");
})

test('sut transforms "hello    world" to "hello world"', () => {
    const actual = sut("hello    world");
    expect(actual).toBe("hello world");
})

test('sut transforms "hello   world" to "hello world"', () => {
    const actual = sut("hello   world");
    expect(actual).toBe("hello world");
})

{% endhighlight %}

<br>

### 반복되는 코드를 for loop 를 사용해서 줄여본다.
{% highlight javascript %}
for(const source of ['hello  world', 'hello   world', 'hello    world']) {
    const actual = sut(source);
    expect(actual).toBe("hello world");
}
{% endhighlight %}

<br>

**위 코드의 문제점**
- 코드량이 많이 줄어들었다.
- 실패에 대한것은 동일하게 나오나 피드백 품질이 낮아졌다.
- 중간에 테스트 케이스가 실패하면 뒤의 테스트 케이스는 실행하지 않기 때문에 그 뒤의 테스트 결과를 장담할 수 없다.

<br>

### Parameterized Test 로 작성

**Parameterized Test 란?**
> 테스트코드를 실행할때 동일한 테스트 코드를 여러 테스트 데이터를 변경해가면서 테스트 하는 기법

**Jest 에서 지원하는 each 를 사용해서 Parameterized Test 구현**
{% highlight javascript %}
test.each`
    source              | expected
    ${"hello  world"}   | ${"hello world"}
    ${"hello   world"}  | ${"hello world"}
    ${"hello    world"} | ${"hello world"}
`('sut transforms "$source" to "$expected"', ({ source, expected }) => {
    const actual = sut(source);
    expect(actual).toBe(expected);
})
{% endhighlight %}

<br>

**기대할 수 있는 장점**
- 코드 중복 가능
- 피드백 품질 높일 수 있음

<br>

## 느낀점
테스트 코드작성시 보일러플레이트를 줄이기 위해 중복되는 부분을 함수로 분리해서 테스트 한적은 있으나 Parameterized Test 에 대해서는 처음 들어봤다.
Parameterized Test 를 지원하다면 단순하면서 비슷한 테스트에 대해서 작성하면 유용할것 같다.


<br>
<br>

[<< 코드 분해](./2-basic-tdd-3-decomposition-code)

<br>

## 참고
[Code 1-2: UnitTest](https://github.com/LeeYoonSam/InitiateTDDHandsOn/tree/main/TEXT-REFINER)

[패스트 캠퍼스 - The RED: 이규원의 현실 세상의 TDD: 안정감을 주는 코드 작성 방법.](https://www.fastcampus.co.kr/dev_red_ygw)

[TDD HandsOn](https://github.com/gyuwon/TDDHandsOn)