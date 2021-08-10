## Regular Expression
###### check special character is double dot
```js
e.target.value = e.target.value.replace(/(\.\.)/,".");
```
###### check first character is number
```js
e.target.value = e.target.value.replace(/^[^0-9]/g,"");
```
###### IP address form
```js
function ipRegExp(e) {
	e.target.value = e.target.value.replace(/[^0-9.]/g, ""); // check number and dot
	e.target.value = e.target.value.replace(/(\.\.)/gi, "."); // check double dot
	e.target.value = e.target.value.replace(/^[^0-9]/g, "");  // check first value is number
	e.target.value = e.target.value.replace(/(\d{3})\d{1}/, "$1"); // limit character length 3 before dot
}
```
###### LATITUDE / LONGITUDE form
```js
function floatRegExp(e) {
	e.target.value = e.target.value.replace(/[^0-9.]/g, ""); // check number and dot
	e.target.value = e.target.value.replace(/(\.\.)/gi, "."); // check double dot
	e.target.value = e.target.value.replace(/^[^0-9]/g, "");  // check first value is number
	e.target.value = e.target.value.replace(/(\d{3})\d{1}/, "$1"); // limit character length 3 before dot
	e.target.value = e.target.value.replace(/(\.\d{2})\d{1}/, "$1"); // limit character length 2 after dot
}
```
###### Korean Name form
```js
function koreanNameRegExp(e) {
	e.target.value = e.target.value.replace(/[^ㄱ-ㅎ|ㅏ-ㅣ|가-힣]/gi,"");
	e.target.value = e.target.value.replace(/(\D{10})(\D{1})/, "$1");
}
```
###### Phone form
```js
function phoneRegExp(e) {
	e.target.value = e.target.value.replace(/[^0-9]/gi,"");
	e.target.value = e.target.value.replace(/(\d{3})(\d{4})(\d{4})/, "$1-$2-$3");
}
```
###### ID form
```js
function idRegExp(e) {
	e.target.value = e.target.value.replace(/[^a-z|0-9]/gi,"");
}
```
###### special character dot(.)
- `dot(.)` means any character when used alone
- usually `dot(.)` is used with `\` for example `\.`
  
###### number / not a number
- we have to use `\d` when checked only number
- we have to use `\D` when checked except number
  
###### remove white space
```js
function removeWhiteSpaceRegExp(e) {
	e.target.value = e.target.value.replace(/ /g, ""); // remove white space
}
```
  
###### currency
```js
function currencyRegExr(e) {
	e.target.value = e.target.value.replace(/^0/, "");
	e.target.value = e.target.value.replace(/[^0-9|]/g, "");
	e.target.value = e.target.value.replace(/(\d)(?=(\d{3})+(?!\d))/g, "$1,");
}
```

###### currencyWithDecimal
```js
/**
 * @description 숫자 입력시 : 각 세자리 수 마다 콤마와 소수점(두자리) 포맷
 * @summary 숫자로 표현되는 대부분의 값에 적용
 */
function comma(value) {
    return (
        // 입력값 : [문자열] 타입으로 변환
        String(value)
            .replace(/^00/, "0")                       // 맨 앞자리 입력에서 "0"이 연속으로 입력 되었을 경우 : "0" 하나로 대체
            .replace(/[^0-9|.]/g, "")                  // [숫자]와 [마침표]만 입력 가능
            .replace(/^[.]/g, "0.")                    // 맨 앞자리 입력에서 [마침표] 입력시 "0"을 앞자리에 배치
            .replace(/^(\d*\.?)|(\d*)\.?/g, "$1$2")    // [마침표]는 최대 하나만 허용
            .replace(/(\d)(?=(\d{3})+(?!\d))/g, "$1,") // 각 세자리 수 마다 [콤마] 삽입
            .replace(/(\.\d{2})\d{1}/, "$1")           // [소수점]은 최대 두자리로 제한
    );
}

export default comma;
```
  
###### email
[Ref.] https://stackoverflow.com/questions/46155/how-to-validate-an-email-address-in-javascript  
  
###### input variable to pattern
```js
function makeParams(query) {
    const searchCondition = {};
    const pagingCondition = {};

    const { name, address, gender, generation, married, faithState, skip, limit} = query;

    // set only search parameter
    if (name) {
        searchCondition.name = new RegExp(name, "i");
    }
    if (address) {
        searchCondition.address1 = new RegExp(address, "i");
    }
    if (gender) {
        searchCondition.gender = new RegExp(gender, "i");
    }
    if (generation) {
        searchCondition.generation = new RegExp(generation, "i");
    }
    if (married) {
        searchCondition.married = new RegExp(married, "i");
    }
    if (faithState) {
        searchCondition.faithState = new RegExp(faithState, "i");
    }

    // set only paging parameter
    if (skip) {
        pagingCondition.skip = Number((page - 1) * query.limit);
    }
    if (limit) {
        pagingCondition.limit = Number(limit);
    }

    return {
        searchCondition,
        pagingCondition,
    };
}
```
  
