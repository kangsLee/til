# TextView

## ellipsize
글자가 길어 다 보여주지 못할 경우 ellipsize를 사용한다.
`android:singleLine="true"` 혹은 `android:maxLines="n"`과 함께 사용한다.

- `android:ellipsize="none"` 아무런 속성도 없음
- `android:ellipsize="start"` 글자의 앞 부분이 ...으로 표시 된다.
- `android:ellipsize="end"` 글자의 뒷 부분이 ...으로 표시 된다.
- `android:ellipsize="middle"` 글자의 중간 부분이 ...으로 표시 된다.
- `android:ellipsize="marquee"` 글자가 오른쪽에서 왼쪽으로 흘러간다. (마퀴태그)
 
> 마퀴는 selected 또는 focus가 되어있어야 정상 작동하므로, 작동하지 않을 경우 setSelected(true)로 설정한다. 