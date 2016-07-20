# Firebase Messaging

### Gradle Setting
```gradle
compile "com.google.firebase:firebase-messaging:${version.firebase}"
```

### Service Register [ Manifests ]
```xml
 <service android:name=".fcm.FCMInstanceIDService">
            <intent-filter>
                <action android:name="com.google.firebase.INSTANCE_ID_EVENT" />
            </intent-filter>
        </service>
        <service android:name=".fcm.FCMMessagingService">
            <intent-filter>
                <action android:name="com.google.firebase.MESSAGING_EVENT" />
            </intent-filter>
        </service>

```
- Firebase Key, Firebase Message 수신을 위해 Service를 등록한다
 

### FirebaseInstanceId Service
```java
@Override
    public void onTokenRefresh() {
        String refreshedToken = FirebaseInstanceId.getInstance().getToken();
        Log.d("FCMInstanceService", "Refreshed token: " + refreshedToken);
    }
```
### Firebase Messaging Service
```java
@Override
public void onMessageReceived(RemoteMessage remoteMessage) {
    super.onMessageReceived(remoteMessage);
    
    // Notification 등록
    RemoteMessage.Notification notification = remoteMessage.getNotification();
    NotificationUtils.sendNotification(this, notification.getTitle(), notification.getBody());
}
```

- Firebase Console - Notifications에서 아래의 내용을 참고하여 원하는 푸시 내용을 보낼 수 있다. 
- RemoteMessage.Notification 참고 
 https://firebase.google.com/docs/reference/android/com/google/firebase/messaging/RemoteMessage.Notification

