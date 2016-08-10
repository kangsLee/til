# Firebase Remote Config

## 초간단 사용법
- 기본 Url이 Google인 링크를 Facebook으로 설정해보기.

### 1. Gradle Setting
```gradle
compile 'com.google.firebase:firebase-config:${version.firebase}"
```

### 2. Singleton Remote Config 얻어오기
```java
 config = FirebaseRemoteConfig.getInstance();
```

### 3. Default Value를 xml에 정의해두기
- res/xml/xxxxx.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<defaultsMap>
    <entry>
        <key>url_link</key>
        <value>https://www.google.com</value>
    </entry>
</defaultsMap>
```

### 4. xml을 config에 설정 하기
```java
config.setDefaults(R.xml.xxxxx);
```

### 5. 값 셋팅하기 
```java
final String ~ URL_LINK = "url_link;
url = config.getString(URL_LINK);
```

### 6. Firebase Config Data Fetch 해보기
```java
long cacheExpiration = 3600;
        config.fetch(cacheExpiration)
                .addOnCompleteListener(new OnCompleteListener<Void>() {
                    @Override
                    public void onComplete(@NonNull Task<Void> task) {
                        if (task.isSuccessful()) {
                            Log.d(TAG, "Fetch Succeeded");
                            config.activateFetched();
                        } else {
                            Log.d(TAG, "Fetch failed");
                        }
                        url = config.getString(URL_LINK);
                    }
                });
```

- https://console.firebase.google.com/project/project-name/config 에서   
매개변수 url_link를 추가하고 '변경사항 게시'를 누르게 되면 값이 변경되게 된다.  
또한 Fetch를 수행하고 3600초간은 해당 값을 유지하게되므로 용도에 맞게 적절하게 사용하면 된다.


## 개발자모드
- 개발자 모드를 추가하여 사용하면 Config Value 테스트에 용이하다.
- ex ) cacheExpiration값을 0로 설정하여 테스트

### ConfigSetting 추가
```java
FirebaseRemoteConfigSettings configSettings = new FirebaseRemoteConfigSettings.Builder()
         .setDeveloperModeEnabled(BuildConfig.DEBUG)
         .build();
 config.setConfigSettings(configSettings);
```

### cacheExpiration 시간 조절하기
```java
if (config.getInfo().getConfigSettings().isDeveloperModeEnabled()) {
            cacheExpiration = 0;
        }
```

- Firebase Remote Config Page
 https://firebase.google.com/docs/remote-config/

