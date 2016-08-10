# Firebase Dynamic Link

### Gradle Setting
```gradle
compile "com.google.firebase:firebase-invites:${version.firebase}"
```

### Dynamic Link 생성하기
 1. [Firebase Console](https://console.firebase.google.com/)에 접속한다.
 2. Project Settings 페이지에서 안드로이드 SHA-1 값을 등록한다.
 3. Console 왼쪽 메뉴에서 다이나믹 링크를 클릭하여, 다이나믹링크 관리 페이지에 접속한다.
 4. `새 동적링크 버튼`을 누르고 폼을 채운 후 `링크 만들기`를 누르면 생성된다.

### Dynamic Link를 직접 만들어보기

```
 https://domain/?link=your_deep_link&apn=package_name[&amv=minimum_version][&ad=1][&al=android_link][&afl=fallback_link]
```
- 위에서 동적링크를 생성할 때 나온  도메인을 사용함.
- 자세한 파라미터들은 하단 링크를 참조한다.

### Intent-filter 추가 [ Manifests ]
```xml
<activity ...
 <intent-filter>
                 <action android:name="android.intent.action.VIEW" />
 
                 <category android:name="android.intent.category.DEFAULT" />
                 <category android:name="android.intent.category.BROWSABLE" />
 
                 <data
                     android:host="도메인주소"
                     android:pathPrefix="/path" 
                     android:scheme="http" />
                 <data
                     android:host="도메인주소"
                     android:pathPrefix="/path"
                     android:scheme="https" />
             </intent-filter>
</activity>
```
- pathPrefix는 도메인주소/path로 들어온 딥링크만 필터링한다.
- [DeepLinking 알아보기](https://developer.android.com/training/app-indexing/deep-linking.html)

### Activity 처리
```java
Uri uri = intent.getData(); // uri를 가져와서 
 // uri.getPath()
 // uri.getQuery() 등으로 처리한다. 
```


- Firebase Dynamic Links on Android 참고 
 https://firebase.google.com/docs/dynamic-links/android

