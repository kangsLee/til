# 크롬 커스텀 탭으로 더 빠르게 웹을 보여주기
앱 내부에서 링크를 자연스럽게 연결시키면서 빠르게 보여주고 싶다면, 크롬 커스톰 탭 사용해보자!

## 크롬, 커스텀탭, 웹뷰 비교
![](https://developer.chrome.com/multidevice/images/customtab/performance.gif)

## 초간단 사용법
직접 구현해도 되지만, 간단하고 빠르게 사용해볼 것이므로 Google 데모에 있는 CustomTabActivityHelper를 사용한다.

- [Google 데모 깃헙 링크](https://github.com/GoogleChrome/custom-tabs-client/tree/master/demos)

#### gradle setting
    compile "com.android.support:customtabs:${version.supportLibrary}"


#### CustomTabService 연결 
``` java
private CustomTabActivityHelper customTabActivityHelper;

    CustomTabActivityHelper = new CustomTabActivityHelper();
     // 연결이 완료되었을 때 Callback을 받고 싶다면 ConnectionCallback을 implements한다.
    customTabActivityHelper.setConnectionCallback (this); 

    @Override 
    public void onStart()  { 
        super.onStart(); 
        customTabActivityHelper.bindCustomTabsService(this); 
    }

    @Override 
    public void onStop()  { 
        super.onStop();
        customTabActivityHelper.unbindCustomTabsService(this); 
    }     
```

#### CustomTab 오픈
```kotlin
val intentBuilder = CustomTabsIntent.Builder()
    intentBuilder.setToolbarColor(Color.WHITE)
    intentBuilder.setSecondaryToolbarColor(Color.BLACK)

    intentBuilder.setShowTitle(true)

    intentBuilder.enableUrlBarHiding()

    intentBuilder.setStartAnimations(context, R.anim.slide_in_right, R.anim.slide_out_left)
    intentBuilder.setExitAnimations(context, android.R.anim.slide_in_left, android.R.anim.slide_out_right)

    CustomTabActivityHelper.openCustomTab(
            context as Activity, intentBuilder.build(), Uri.parse(url), WebViewFallback())
```
> 색상설정 및 타이틀 표시유무, UrlBar 활성화 유무와 애니메이션 효과 등.. 다양한 설정을 넣어줄 수 있다.

- [크롬 커스텀 탭 자세히 알아보기](https://developer.chrome.com/multidevice/android/customtabs#warm-up%20chrome%20to%20make%20pages%20load%20faster)