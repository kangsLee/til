# xmlns:android 기본 애트리뷰트

## nestedScrollingEnabled
ScrollView 안에 Recyclerview가 포함되어 있다면, 스크롤이 부드럽지 못하고 툭툭 걸리게 된다.
그 때 `recyclerView`에 `nestedScrollingEnabled = false`를 적용해주면 전체적으로 부드럽게 스크롤이 된다.

`android:nestedScrollingEnabled="false"`