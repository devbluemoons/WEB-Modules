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
  
###### email
[Ref.] https://stackoverflow.com/questions/46155/how-to-validate-an-email-address-in-javascript  
  
###### input variable to pattern
```js
function makeParams(query) {
    const searchCondition = {};
    const pagingCondition = {};

    // set only search parameter
    if (query.name) {
        searchCondition.name = new RegExp(query.name, "i");
    }
    if (query.address) {
        searchCondition.address1 = new RegExp(query.address, "i");
    }
    if (query.gender) {
        searchCondition.gender = new RegExp(query.gender, "i");
    }
    if (query.generation) {
        searchCondition.generation = new RegExp(query.generation, "i");
    }
    if (query.married) {
        searchCondition.married = new RegExp(query.married, "i");
    }
    if (query.faithState) {
        searchCondition.faithState = new RegExp(query.faithState, "i");
    }

    // set only paging parameter
    if (query.skip) {
        pagingCondition.skip = Number((query.page - 1) * query.limit);
    }
    if (query.limit) {
        pagingCondition.limit = Number(query.limit);
    }

    return {
        searchCondition,
        pagingCondition,
    };
}
```
  
