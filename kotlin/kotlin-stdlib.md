# 코틀린 stdlib 
[Kotlin References](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/)

## function block 4가지
코틀린을 사용하면서 `let with run apply` 의 사용을 조금 더 확실하게 하고자 정리해본다.

### let
```
 val _let = "str".contains("s").let {
                it.not()
            }
```
- "str".contains의 결과 값을 it로 받을 수 있다.
- it.not()를 반환한다.

### with
``` kotlin
with(slider) {
    duration = 3000
    animation = ANIM_LEFT
}
```
- slider.duration, slider.animation과 같은 작업을 duration, animation으로 작성 가능하다.
- 마지막 줄의 반환 값을 반환한다.

### run
```
 val _run = str?.run {
                contains("s")
            }
```

- "str"에 바로 접근 가능하다.
- contains("s")의 결과를 반환한다.
- `with`와 비슷하나 엘비스 연산자로 null check가 가능하다.

### apply
``` kotlin
val frag = MyUtils.apply { id = "xxxx1" }
// id가 xxxx1로 초기화 된 val frag: MyUtil
```
- 초기화 할 때 주로 사용
- MyUtils에 접근 가능하다.
- MyUtils를 반환한다.
