# 코틀린으로 간단하게 슬랙훅을 날려보는 예제
- `Dagger, Retrofit, RxJava, Gson`을 이용하여 Slack에 훅을 날려보자
- **준비사항**으로는 슬랙 Custom Integrations Incoming WebHooks에서 Webhook URL을 가져와야한다.

```kotlin
// SlackHook.kt / 훅 모델
class SlackHook{
    var channel: String
    var username: String
    var text: String
    var icon_emoji: String? = null

    constructor(channel: String = "#_general", username: String = "Android", text: String, icon_emoji: String? = ":android:"){
        this.channel = channel
        this.username = username
        this.text = text
        this.icon_emoji = icon_emoji
    }

    override fun toString(): String {
        return Gson().toJson(this)
    }
}
```
> 채널, 봇 이름, 아이콘은 기본값이 있으므로 파라미터를 넘기지 않아도 되지만 메시지 내용은 필수로 받아야한다

- channel : 훅을 받을 채널명
- username : Bot 이름
- text : 메시지 내용
- icon_emoji : 표시 될 아이콘 (android는 사전에 슬랙에 등록한 아이콘)

```kotlin
// xxClient.kt / 통신 클라이언트
@Inject
constructor(okHttpClient: OkHttpClient) {
    val retrofitForSlack = Retrofit.Builder().baseUrl("https://hooks.slack.com/")
                    .addCallAdapterFactory(RxJavaCallAdapterFactory.create())
                    .client(okHttpClient)
                    .build()
                    
slackHookService = retrofitForSlack.create(SlackHookService::class.java)
}

// ----------------------- SlackHookService ---------------------------
fun sendMessageToSlack(slackHook: String): Observable<ResponseBody> {
    return slackHookService.sendMessageToSlack(slackHook)
}
```
> 클라이언트 작성 

```kotlin
// SlackHookService.kt / 서비스 인터페이스
interface SlackHookService {
    @FormUrlEncoded
    @POST("/services/Key.....")
    fun sendMessageToSlack(
            @Field("payload") slackHook: String
    ): Observable<ResponseBody>
}
```
> Service Interface, Slack Hook에서 받은 값을 POST에 넣어준다.

```kotlin
// xxActivity.kt / 실행 할 액티비티 화면
client.sendMessageToSlack(SlackHook(text = "훅 테스트...").toString())
                    .subscribeOn(Schedulers.io())
                    .observeOn(Schedulers.newThread())
                    .subscribe({}, {error -> error.printStackTrace()})
```
> Activity에서 SlackHook 전송. SlackHook(`username, channel, icon_emoji ...`)

