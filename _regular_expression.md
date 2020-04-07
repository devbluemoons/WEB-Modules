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
function ipRexExp(e) {
	e.target.value = e.target.value.replace(/[^0-9|.]/g, ""); // check number and dot
	e.target.value = e.target.value.replace(/(\.\.)/gi, "."); // check double dot
	e.target.value = e.target.value.replace(/^[^0-9]/g, "");  // check first value is number
	e.target.value = e.target.value.replace(/(\d{3})\d{1}/, "$1"); // limit character length 3 before dot
}
```
###### LATITUDE / LONGITUDE form
```js
function floatRexExp(e) {
	e.target.value = e.target.value.replace(/[^0-9|.]/g, ""); // check number and dot
	e.target.value = e.target.value.replace(/(\.\.)/gi, "."); // check double dot
	e.target.value = e.target.value.replace(/^[^0-9]/g, "");  // check first value is number
	e.target.value = e.target.value.replace(/(\d{3})\d{1}/, "$1"); // limit character length 3 before dot
	e.target.value = e.target.value.replace(/(\.\d{2})\d{1}/, "$1"); // limit character length 2 after dot
}
```
###### special character dot(.)
- `dot(.)` means any character when used alone
- usually `dot(.)` is used with `\` for example `\.`
