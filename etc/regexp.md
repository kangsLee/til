#Regexp

##기초
- `?` 최대 1회까지 문자를 허용함 (abc?e) = (abe) = (abce)  
- `+` 1회 이상 문자를 허용함 (abc+e) = (abce) = (abcce) = (abcccccccce)  
- `*` 0회 이상 까지 문자를 허용함 (abc*e) = (abe) = (abccccccccce) 
- `g` 모든 패턴에 대해 전역으로 검색한다.
- `i` 대소문자를 구분하지 않음.
 
### hubot을 사용하며 coffeescript에서 사용해 본 예
```coffeescript
/메모\s*(제거|삭제|지우기|지워줘) (\d+)/i
```

- `\s*` 스페이스바를 써도 되고 안써도 된다.
- `(|)` 괄호 안에 하나라도 일치하는지
- `(\d+)` 숫자가 하나 이상 써져있는지

### replace와 정규식을 사용하여 replaceAll과 같은 효과를 내보기
```js
js 
 'zzz.z.z'.replace(/\./g, "_")
 
coffeescript
 'zzz.z.z'.replace /\./g, "_"
```
문자 내의 모든 .을 _로 대체하는 코드 


참고한 사이트
 https://ko.wikipedia.org/wiki/%EC%A0%95%EA%B7%9C_%ED%91%9C%ED%98%84%EC%8B%9D 
