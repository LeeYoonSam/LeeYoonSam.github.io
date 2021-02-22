---
layout: post
title:  "Kotlin 빌더 패턴 고차함수로 전달받아서 간편하게 만들기"
categories: kotlin
---

# Kotlin 빌더 패턴 고차함수로 전달받아서 간편하게 만들기

### User 클래스
{% highlight kotlin %}
data class User(
	val id: Int,
	val name: String
)
{% endhighlight %}

### User 클래스의 빌더 클래스
{% highlight kotlin %}
class UserBuilder {
    var id: Int = 0
    var name: String = ""
    
    fun append(id: Int): UserBuilder {
        this.id = id
        return this
    }
    
    // 없어도 되지만 여러가지 테스트 해보기위해 추가
    fun appendId(id: Int): UserBuilder {
        this.id = id
        return this
    }
    
    fun append(name: String): UserBuilder {
     	this.name = name
        return this
    }
    
    // 없어도 되지만 여러가지 테스트 해보기위해 추가
    fun appendName(name: String): UserBuilder {
     	this.name = name
        return this
    }
    
    fun build(): User {
        return User(id, name)
    }
}
{% endhighlight %}

### 빌더를 사용하는 고차함수 전달받기
{% highlight kotlin %}
fun buildUser(buildBlock: UserBuilder.() -> Unit): User {
    val builder = UserBuilder()
    builder.buildBlock()
    return builder.build()
}
{% endhighlight %}

### 빌더 패턴 사용하기
{% highlight kotlin %}
fun main() {
    val user1 = UserBuilder().append(1).append("albert").build()
    println(user1)
    
    val user2 = buildUser {
        append(2)
        append("albert2")
    }
    println(user2)
    
    val user3 = buildUser {
        appendId(3)
        appendName("albert3")
    }
    println(user3)
}


>>> User(id=1, name=albert1)
>>> User(id=2, name=albert2)
>>> User(id=3, name=albert3)
{% endhighlight %}

<br/>
<br/>

[Kotlin koans](https://play.kotlinlang.org/koans/Builders/String%20and%20map%20builders/Task.kt) 의 Builder 부분을 보다가 생각나서 한번 시도해봤다.
koans 에는 StringBuilder, HashMap 등을 사용한 예제가 나와있다.

<br/>
<br/>

-> [Code 보러가기](https://pl.kotl.in/QeZ6FQg_L)
