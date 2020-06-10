###### attribute
- `on` : 폼 양식의 입력값을 기억하여 다시 채워줌
- `off` : 폼 양식의 입력값을 기억하지 않는다 
```html
<form autocomplete="off"></form>
```
  
###### checkbox
```html
<input type="checkbox" id="remember" name="remember"><label for="remember"><span></span>Remember ID</label>
```
```js
document.querySelector("input[name=remember]").addEventListener("click", e => {
	console.log(e.target.checked);
});
```
