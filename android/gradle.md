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
