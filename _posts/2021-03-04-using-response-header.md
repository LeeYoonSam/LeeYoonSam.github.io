---
layout: post
title:  "Response Header 에서 값을 가져오기 with Retrofit, MockWebServer"
categories: kotlin
---

Response 로 받는 body 데이터 외에 Header 에 오는 데이터를 사용하는 방법을 알아 봅니다.

실제 데이터 대신 MockWebServer 를 대신 사용해서 Response 및 Header 데이터를 생성하고 가져오는 테스트를 합니다.

<br>

### app/build.gradle
{% highlight gradle %}
dependencies {
    testImplementation("com.squareup.okhttp3:mockwebserver:4.9.0")
}
{% endhighlight %}

- mockwebserver 디펜던시 추가

<br>

### SampleResponse
{% highlight kotlin %}
data class SampleResponse(
  val id: Long,
  val name: String
)
{% endhighlight %}

- 간단한 Response 객체 생성

<br>

### Api Interface
{% highlight kotlin %}
interface Api {
    @GET("sample")
    fun getSample(): Call<SampleResponse>
}
{% endhighlight %}

- API 호출에 사용할 샘플 추가


<br>

### 전체 코드
{% highlight kotlin %}
class ApiHeaderParsingTest {
    private val server: MockWebServer = MockWebServer()
    private lateinit var api: Api
    
    private val lock: CountDownLatch = CountDownLatch(1)

    @Before
    fun init() {
        server.start()
        val interceptor = HttpLoggingInterceptor()
        interceptor.level = HttpLoggingInterceptor.Level.BODY

        val client = OkHttpClient.Builder()
                .addInterceptor(ExceptionInterceptor())
                .addInterceptor(interceptor)

        api = Retrofit.Builder()
            .baseUrl(server.url("/"))
            .addConverterFactory(provideConverterFactory())
            .client(client.build())
            .build()
            .create(Api::class.java)
    }

    private fun provideConverterFactory(): Converter.Factory {
        return MoshiConverterFactory.create(
            Moshi.Builder()
                .add(KotlinJsonAdapterFactory())
                .build()
        )
    }

    @Test
    fun `Get Response Header Test`() {

        // Assign
        val response = MockResponse()
            .setResponseCode(HttpURLConnection.HTTP_OK)
            .setHeader("group", "a")
            .setBody(FixtureResponse.Sample)

        server.enqueue(response)

        val result = api.getSample()
        result.enqueue(object : Callback<SampleResponse> {
            override fun onResponse(
                call: Call<SampleResponse>,
                response: Response<SampleResponse>
            ) {
                // get headers
                val headers = response.headers()

                val group = headers.get("group")
                println("group: $group")

                Assert.assertEquals(group, "a")
            }

            override fun onFailure(call: Call<SampleResponse>, t: Throwable) {
                TODO("Not yet implemented")
            }
        })

        // 테스트 함수가 지속되도록 딜레이
        lock.await(5000, TimeUnit.MILLISECONDS)
    }

    @After
    fun shutdown() {
        server.shutdown()
    }
}
{% endhighlight %}

- Retrofit 의 Call 을 사용해서 Response 를 받게한다.
- CallBack 을 통해서 response.getHeaders() 에 전달된 header 정보를 가져온다.
- header 의 get 함수를 통해서 필요한 헤더 정보를 가져온다.
{% highlight java %}
/** Returns the last value corresponding to the specified field, or null. */
  public @Nullable String get(String name) {
    return get(namesAndValues, name);
  }
{% endhighlight %}

<br/>
<br/>

## 참고

[MockWebServer](https://github.com/square/okhttp/tree/master/mockwebserver)
