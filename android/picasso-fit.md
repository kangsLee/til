# 피카소 fit()을 사용하여 메모리를 절약하자
Glide를 사용하지 않고 Picasso를 사용한다면 원본 해상도를 가져오기에 OOM이 발생할 수 있다.
Glide와 같이 필요한 사이즈의 이미지를 로드하여 메모리를 절약해보자.

- 기본 사용법

```java
Picasso.with(this).load(imageUrl).into(imageView);
```

- fit을 사용하여 메모리를 절약

```java
picasso.load(imageUrl).fit().into(imageView);
```

- 이미지 사이즈가 고정이 아닌 동적 사이즈라면?
 
1. xml attribute 설정

```xml
android:layout_width="match_parent"
android:layout_height="match_parent"
android:adjustViewBounds="true"
```

2. centerInside() 추가

```java
picasso.load(imageUrl).fit().centerInside().into(imageView);
```