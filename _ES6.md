###### const, let
  
`ES6` 문법을 사용한다면 `var` 키워드로 변수 선언을 하지 않는 것이 좋다
  
`const` - 상수의 역할로서 재할당을 금지한다
  
`let` - 변수로서 재할당이 가능하다  
  
기본적으로 `const`를 사용하고 재할당이 필요한 변수의 경우에만 `let`을 사용한다  
  
###### ref.
https://poiemaweb.com/es6-block-scope
  
---
  
###### import, export
```js
import * as [class-name] from @/js-file-name;
//example
import * as date from @/utilDateAndTime;

export function[function-name](){} /* or */ const [variable-name]
//example
export function currentTime(){}
export const date = (...);
export let abc = (...)
```
  
###### check variable
```js
typeof [variable-name] !== "undefined"
//example
if(typeof rowData !== "undefined"){}
```
