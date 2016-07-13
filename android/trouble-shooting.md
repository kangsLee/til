#Trouble Shooting !
- 각종 예외와 해결법 정리 

## Fragment 
- `Can not perform this action after onSaveInstanceState`
    - 상황  
        - ViewPager, SupportMapFragment
        - GoogleMap이 포함 된 Fragment와 일반페이지를 매우 빠르게 전환
        - DestroyView에서 GoogleMap을 `remove.commit` 해주는 상황
    - 해결책
        - `commit()`을 `commitAllowingStateLoss()`으로 변경. (상태값과 무관한 동작에서만 사용)
        - `viewpager.setOffscreenPageLimit`을 이용하여 페이저내 Fragment를 유지시킨다.
          (상황에따라 Fragment가 유지되지 않을 수 있어, 예외가 발생할 수 있음)  
        
    
    
   