# 코틀린 stdlib 
[Kotlin References](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/)

## function block 4가지
코틀린을 사용하면서 `let with run apply` 의 사용을 조금 더 확실하게 하고자 정리해본다.

### let
`inline fun <T, R> T.let(block: (T) -> R): R (source)`
>Calls the specified function block with this value as its argument and returns its result.

```
 val _let = "str".contains("s").let {
                it.not()
            }
```
- "str".contains의 결과 값을 it로 받을 수 있다.
- it.not()를 반환한다.

### with
`inline fun <T, R> with(receiver: T, block: T.() -> R): R (source)`
>Calls the specified function block with the given receiver as its receiver and returns its result.

``` kotlin
with(slider) {
    duration = 3000
    animation = ANIM_LEFT
}
```
- slider.duration, slider.animation과 같은 작업을 duration, animation으로 작성 가능하다.
- 마지막 줄의 반환 값을 반환한다.

### run
`inline fun <R> run(block: () -> R): R (source)`
>Calls the specified function block and returns its result.

```
val _run = run {
    val item = getItem()
    item.name = "good"
    item.power = 3000
    item.name
}
```
- 특정 로직을 수행하고 마지막 줄을 반환시킬 수 있다.
- 아무런 반환값을 주지 않아도 된다.

`inline fun <T, R> T.run(block: T.() -> R): R (source)`
> Calls the specified function block with this value as its receiver and returns its result.

```
 val _run = str?.run {
                contains("s")
            }
```

- "str"에 바로 접근 가능하다.
- contains("s")의 결과를 반환한다.
- `with`와 비슷하나 엘비스 연산자로 null check가 가능하다.

### apply
`inline fun <T> T.apply(block: T.() -> Unit): T (source)`
> Calls the specified function block with this value as its receiver and returns this value.

``` kotlin
val frag = MyUtils.apply { id = "xxxx1" }
// id가 xxxx1로 초기화 된 val frag: MyUtil
```
- 초기화 할 때 주로 사용
- MyUtils에 접근 가능하다.
- MyUtils를 반환한다.
