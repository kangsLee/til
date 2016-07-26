# 안드로이드 크래시 리포트 도구들, 초간단 이용방법

## Firebase Crash Report

### Gradle Setting
```gradle
compile "com.google.firebase:firebase-crash:${version.firebase}"
```

### 첫 크래시 생성
```java
FirebaseCrash.report(new Exception("My first Android non-fatal error"));
```

- Firebase Crash Report는 정말 간단하게 Gradle을 추가해 주는 것으로 크래시를 잡아내고 리포트 할 수 있다.

### 확인 
크래시 확인은 [FirebaseConsole](https://console.firebase.google.com/) 왼쪽 사이드바에서 Crash를 선택하여 확인할 수 있다. 

## Crashlytics ( Fabric )

* 우선 [가입하기](https://fabric.io/sign_up?signup_campaign_id=https://get.fabric.io&locale=ko)를 통해 회원가입을 한다. 

### 설정 및 이용
- AndroidStudio - Preferences - Plugins - Browse Repositories - `'Fabric' 검색`
- 재부팅 후 오른쪽에 Fabric이 나타난 것을 확인.
- 로그인 후 Crashlytics 클릭하여 자동 설정 및 수동 설정을 해준다.
- 크래시가 발생하면 메일에 정보가 날아온다.
- 추가로 Crashlytics App을 설치하면 외부에서도 쉽게 크래시 정보를 받아볼 수 있다.