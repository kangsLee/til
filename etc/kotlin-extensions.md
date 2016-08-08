# 코틀린에서 함수를 입 맛대로 추가해보기
코틀린에서는 한 클래스 내에 한정 된 함수를 확장시켜 원하는 함수를 추가하여 사용할 수 있도록 Extension functions를 제공한다.
 
만약 AppCompatActivity에서 Toast를 자주 사용하고 있다면 아래와 같이 추가해볼 수 있다.

```kotlin
fun AppCompatActivity.toast(message: String, duration: Int = Toast.LENGTH_SHORT) {
    Toast.makeText(this, message, duration).show()
}
```
```kotlin
fun AppCompatActivity.toast(@StringRes message: Int, duration: Int = Toast.LENGTH_SHORT) {
    Toast.makeText(this, message, duration).show()
}
```
> AppCompatActivity를 상속받은 클래스에서 toast("메시지")를 입력하면 Toast를 보여줄 수 있다.

자주쓰이는 함수를 간결하게 작성하거나, `String`이나 `Int` 등에서 문자를 포매팅할 때 등 여러 곳에서 유용하게 쓰여 꼭 사용해야 할 기능이지 않나 싶다.

`* Swift Extensions`도 있다.