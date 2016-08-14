# 마퀴 속성을 사용하며 생긴 이슈 정리

## 구성
 
- View hierarchy

```
ViewPager
 ScrollView
  MarqueeFragment
```

> View 구조 

- XML

```xml
 <TextView
            android:ellipsize="marquee"
            android:focusable="true"
            android:marqueeRepeatLimit="marquee_forever"
            android:singleLine="true"
            android:maxLines="1" />
```

> 마퀴를 사용 하기 위해 기본 xml을 설정

## 문제
1. ViewPager 내 마퀴가 작동하지 않음
- ViewPager가 생성 될 때 View가 완전히 구성되지 않은 상태에서 포커스를 설정함
- subscribe를 이용하여 view가 완전히 구성되고 나서 textview에 focus를 설정해줌.
- view.postDelayed로 설정해도 된다.

2. ViewPager가 전환 되면서 스크롤이 상단으로 이동 됨
- 마퀴를 사용하기 위해 focus를 주었기 때문에 발생함
- NestedScrollView 또는 ScrollView를 상속받아 `onRequestFocusInDescendants`를 override 하여 return값을 `true`로 반환시켜준다.