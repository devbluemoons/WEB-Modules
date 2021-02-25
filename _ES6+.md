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

// 함수를 내보낼 순 없다, 모듈 또는 컴포넌트만 가능
default export [only module]
```
  
###### check variable
```js
typeof [variable-name] !== "undefined"
//example
if(typeof rowData !== "undefined"){}
```
  
###### spread operator
```js
// array
const arr = [...data, 111, 222, 333];
// object
const obj = {...data, aaa:111, bbb:222, ccc:333};

const obj01 = {
  aaa: 111,
  bbb: 222,
  ccc: 333,
  ddd: null,
  eee: null,
};

const obj02 = {
  ddd: 444,
  eee: 555,
};

const sumObj = {...obj01, ...obj02};

const innerObj = {
  aaa: 111,
  bbb: 222,
  ccc: 333,
  obj: {
    ddd: null,
    eee: null,
  }
}

const objA = {
  aaa: 111,
  bbb: 222,
  ccc: 333,
}

const objB = {
  ddd: 444,
  eee: 555,
};

const copyInnerObj = {
  ...objA,
  obj: {
    ...objB,
  },
};
```
  
###### inside function of array / [].includes(param)
```js
const numbers = [1,2,3,4,5];
numbers.includes(1); //true
numbers.includes(7); //false
```

###### spread operator with querySelectorAll
```js
[...document.querySelectorAll('div')].map(x => console.log(x.innerHTML))
```
[Ref.] https://stackoverflow.com/questions/2600343/why-does-document-queryselectorall-return-a-staticnodelist-rather-than-a-real-ar
