###### data type only integer
- chartJS의 data 타입은 항상 `integer` 여야 한다
- 겉보기에 `integer` 값이라도 `string` 타입인지 체크해봐야 한다
  
###### dynamic HTML issue
- `동적`으로 html을 생성하고 `chartJS`를 적용할 경우
- 먼저 html를 생성하는 `loop`를 전부 돌린다
- 그 후 `chartJS`의 `data`를 적용한다
