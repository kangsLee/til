#Gradle

## 버전관리
dependencies에 라이브러리를 추가하다보면 같은 버전으로 사용하는 라이브러리가 있을 수 있다.  
대표적으로 'com.android.support:'가 그렇다. 

```gradle
compile "com.android.support:design:24.0.0"
compile "com.android.support:appcompat-v7:24.0.0"
compile "com.android.support:recyclerview-v7:24.0.0"
compile "com.android.support:cardview-v7:24.0.0"`
```
보통의 경우 이런식으로 추가하고 버전이 업데이트 되면 하나씩 올려주었다.  
하지만 def 혹은 ext를 이용하여 변수를 지정하면 다음과 같이 사용이 가능하다.

```gradle
def version = [
        supportLibrary: '24.0.0',
        retrofit      : '2.1.0',
        firebase      : '9.2.0'
]

compile "com.android.support:design:${version.supportLibrary}"
compile "com.android.support:appcompat-v7:${version.supportLibrary}"
compile "com.android.support:recyclerview-v7:${version.supportLibrary}"
compile "com.android.support:cardview-v7:${version.supportLibrary}"
```

## packagingOptions
여러가지 라이브러리를 적용하고 패키징을 하려고하면 Duplicate files copied in APK META-INF/XXXXXX와 같은 오류가 발생하는 경우가 있다.
그 이유는 아래와 같은 파일들이 여러 라이브러리에 각각 들어있을 수 있기 때문이다.
![](http://i.imgur.com/5rLF0dc.png)

이를 해결하려면 packagingOptions에서 패키징을 하지 않을 파일들을 선택할 수 있다.
```gradle
packagingOptions {
     exclude 'META-INF/NOTICE.txt'
     exclude 'META-INF/LICENSE.txt
     exclude 'META-INF/DEPENDENCIES'
     exclude 'META-INF/NOTICE'
     exclude 'META-INF/LICENSE'
}
```