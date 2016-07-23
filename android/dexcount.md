# Method 갯수를 확인하고 줄여보기
- 안드로이드를 개발하다보면 `65536`개의 메소드 제한에 부딪히는 경우가 있다. `멀티덱스`로 해결이 가능하지만 초기 로딩이 상당히 느려지는 현상이 생길 수 있어 가능하다면 메소드 갯수를 줄여보는 것이 좋다.

## build.gradle 설정
```gradle
buildscript {
    dependencies {
        ...
        classpath 'com.getkeepsafe.dexcount:dexcount-gradle-plugin:0.5.0'
    }
}

apply plugin: 'com.getkeepsafe.dexcount'

```

## 사용법
```terminal
./gradlew assembleDebug
```

## DexCount 확인하기
- csv, txt, html 등 다양한 파일로 제공한다. 
- 경로
`/app/build/outputs/dexcount/`
