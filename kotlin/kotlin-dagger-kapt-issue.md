# Dagger를 사용하면서 발생한 이슈

잘 사용하고 있던 Dagger, Kotlin으로 변경시 코드에 Inject가 포함 될 경우 DaggerComponent를 찾을 수 없다고 한다.
예전에 아무리 삽질을 해보아도 해결책이 보이지 않아 해당 부분만 Java를 유지하여 사용하고 있었는데, 오늘 우연히 문제를 발견하여 Kotlin으로 수정하였음.

## 이슈 및 해결
Java Code 에서 Kotlin Code으로 바꾸던 도중 Dagger Issue가 발생 함.  
이를 해결하기 위해 아래의 절차를 거쳐 최종적으로 문제를 해결하였다.

- kapt generateStubs 추가 

```gradle
kapt {
    generateStubs = true
}
```
> 갑자기 RealmPorxy 오류가 발생하여 Realm 사용 불가
 
- Realm 코드 삭제 

> 갑자기 import 된 파일들 전체를 찾지 못하였다., 

- Clean 후 Run

> 갑자기 실행은 되는데.. DaggerComponent를 찾지 못한다고 한다.  

- 실행은 되는데 죽었으니, 최초에 실행되는 Application Class의 DaggerComponent제거 

> 정상 실행 완료.

## 원인
```
appComponent.inject(this)
```
`build()` 까지 완료하였으나, `inject`를 빼먹었다.  
Dagger에서 코드 하나 실수해도 오류를 뿜었으나 찾기 쉬웠는데.. 이번에는 Java 코드에서 잘 돌아가던게 Kotlin으로 전환하니까 되지 않아서 헤맨 것 같다.  
삽질이 마무리 되어 기쁘다...
