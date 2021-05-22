---
layout: post
title:  "EFFECTIVE JAVA 3/E - 아이템 1: 생성자 대신 정적 팩터리 메서드를 고려하라"
categories: java
---

<img src="/images/effective_java3.png" alt="drawing" style="width:200px;"/>

<br>

> 클라이언트가 클래스의 인스턴스를 얻는 전통적인 수단은 public 생성자다.
<br>
모든 프로그래머가 꼭 알아둬야 할 기법이 하나 더 있다.
<br>
클래스는 생성자와 별도로 정적 팩터리 메서드(static factory method)를 제공할 수 있다.
<br>
그 클래스의 인스턴스를 반환하는 단순한 정적 메서드

<br>

* boolean 기본 타입의 박싱 클래스인 Boolean 에서 발췌한 간단한 예로 기본 타입인 boolean 값을 받아 Boolean 객체 참조로 변환해 준다.
{% highlight java %}
public static Boolean valueOf(boolean b) {
    return b ? Boolean.TRUE : Boolean.FALSE;
}
{% endhighlight %}

> 이 정적 패터리 메서드는 디자인패턴에서의 팩터리 메서드와 다르다.

<br>

## 장점
### 1. 이름을 가질 수 있다.
- BigInteger.probablePrime

<br>

### 2. 호출될 때마다 인스턴스를 새로 생성하지는 않아도 된다.
- Boolean.valueOf(boolean)
- 플라이웨이트 패턴(Flyweight pattern) 과 비슷한 기법

<br>

### 3. 반환 타입의 하위 타입 객체를 반환할 수 있는 능력이 있다.

<br>

### 4. 입력 매개변수에 따라 매번 다른 클래스의 객체를 반환할 수 있다.

<br>

### 5. 정적 팩터리 메서드를 작성하는 시점에는 반환할 객체의 클래스가 존재하지 않아도 된다.
- 서비스 제공자 프레임워크는 3개의 핵심 컴포넌트로 이뤄진다.
    - 구현체 동작 정의: 서비스 인터페이스(service interface)
    - 제공자가 구현체를 등록: 제공자 등록 API(provider registration API)
    - 클라이언트가 서비스의 인스턴스를 얻을 때: 서비스 접근 API(service access API)

    <br>

- 3개의 핵심 컴포넌트와 더불어 종종 쓰이는 네번째 컴포넌트
    - 서비스 인터페이스의 인스턴스를 생성하는 팩터리 객체를 설명: 서비스 제공자 인터페이스(service provider interface)

    <br>

- JDBC 구성
    - Connection: 서비스 인터페이스
    - DriverManager.registerDriver: 제공자 등록 API
    - DriverManager.getConnection: 서비스 접근 API
    - Driver: 서비스 제공자 인터페이스

<br><br>

## 단점
### 1. 상속을 하려면 public 이나 protected 생성자가 필요하니 정적 팩터리 메서드만 제공하면 하위 클래스를 만들 수 없다.
- 상속보다 컴포지션을 사용하도록 유도하고 불변 타입으로 만들려면 이 제약을 지켜야 한다는 점에서 오히려 장점으로 받아들일 수도 있다.

<br>

### 2. 정적 팩터리 메서드는 프로그래머가 찾기 어렵다.
- 생성자처럼 API 설명에 명확히 드러나지 않으니 사용자는 정적 팩터리 메서드 방식 클래스를 인스턴스화할 방법을 알아내야 한다.
- API 문서를 잘 써놓고 메서드 이름도 널리 알려진 규약을 따라 짓는 식으로 문제를 완화해줘야 한다.

<br><br>

## 정적 팩터리 메서드에서 흔히 사용하는 명명 방식
- from: 매개변수를 하나 받아서 해당 타입의 인스턴스를 반환하는 형변환 메서드

{% highlight java %}
Date d = Date.from(instant);
{% endhighlight %}
<br>

- of: 여러 매개변수를 받아 적합한 타입의 인스턴스를 반환하는 집계 메서드 

{% highlight java %}
Set<Rank> faceCard = EnumSet.of(JACK, QUEEN, KING);
{% endhighlight %}
<br>

- valueOf: from 과 of 의 더 자세한 버전 

{% highlight java %}
BigInteger prime = BigInteger.valueOf(Integer.MAX_VALUE);
{% endhighlight %}
<br>

- instance 혹은 getInstance: (매개변수를 받는다면) 매개변수로 명시한 인스턴스를 반환하지만, 같은 인스턴스임을 보장하지는 않는다. 

{% highlight java %}
StackWalker luke = StackWalker.getInstance(options);
{% endhighlight %}
<br>

- create 혹은 newInstance: instance 혹은 getInstance 와 같지만, 매번 새로운 인스턴스를 생성해 반환함을 보장한다. 

{% highlight java %}
Object newArray = Array.newInstance(classObject, arrayLen);
{% endhighlight %}
<br>

- getType: getInstance 와 같으나, 생성할 클래스가 아닌 다른 클래스에 팩터리 메서드를 정의할 때 쓴다. "Type"은 팩터리 메서드가 반환할 객체의 타입이다. 

{% highlight java %}
FileStore fs = Files.getFileStore(path);
{% endhighlight %}
<br>

- newType: newInstance 와 같으나, 생성할 클래스가 아닌 다른 클래스에 팩터리 메서드를 정의할 때 쓴다. "Type"은 팩터리 메서드가 반환할 객체의 타입이다. 

{% highlight java %}
BufferedReader br = Files.newBufferedReader(path);
{% endhighlight %}
<br>

- type: getType 과 newType 의 간결한 버전

{% highlight java %}
List<Complaint> litany = Collections.list(legacyLitany);
{% endhighlight %}
<br>

## 핵심 정리
정적 팩터리 메서드와 public 생성자는 각자의 쓰임새가 있으니 상대적인 장단점을 이해하고 사용하는 것이좋다.
<br>
그렇다고 하더라도 정적 팩터리를 사용하는 게 유리한 경우가 더 많으므로 무작정 public 생성자를 제공하던 습관이 있다면 고치자.