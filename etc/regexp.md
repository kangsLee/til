#Regexp

##기초
- `?` 최대 1회까지 문자를 허용함 (abc?e) = (abe) = (abce)  
- `+` 1회 이상 문자를 허용함 (abc+e) = (abce) = (abcce) = (abcccccccce)  
- `*` 0회 이상 까지 문자를 허용함 (abc*e) = (abe) = (abccccccccce) 
 
- hubot을 사용하며 coffeescript에서 사용해 본 예
```coffeescript
/메모\s*(제거|삭제|지우기|지워줘) (\d+)/i
```

- `\s*` 스페이스바를 써도 되고 안써도 된다.
- `(|)` 괄호 안에 하나라도 일치하는지
- `(\d+)` 숫자가 하나 이상 써져있는지
