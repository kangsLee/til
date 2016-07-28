# Generics + GSON 사용시 리스트 타입 변환

## Issue
`Pageable`로 받아오는 데이터가  대부분이었는데. 클래스를 하나 작성하 재사용하기 위해 `Generics`를 사용하던 중 다음과 같은 이슈가 발생하였다.
`Kotlin`에서 `Generics (<*>, <Any>)`를 사용했을 때 `Gson`으로 변환하여 클래스에 매핑하려고 하면 
*`'com.google.gson.internal.LinkedTreeMap'`* 이슈가 발생한다.  
(Java에서는 <?>를 사용했을 때 동일한 이슈가 발생함)


## Solution

```kotlin
  val type = object : TypeToken<List<클래스>>() {}.type
  val className = Gson().fromJson<List<클래스>>(json... , type)
```