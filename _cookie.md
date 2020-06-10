###### set cookie
```js
function setCookie() {
		
	const cookieName = "userId";
	const userId = document.querySelector("input[name=userId]").value;

	const expireDate = new Date();
	expireDate.setDate(expireDate.getDate() + 7); // cookie에 [userId] 7일동안 보관
	const expires = expireDate.toGMTString();

	const cookieValue = `${escape(userId)}; expires=${expireDate.toGMTString()};`;
	document.cookie = `${cookieName}=${cookieValue};`;
}
```
  
###### get cookie  
```js
function autocompleteUserId() {
	
	const cookieName = "userId";
	const value = `; ${document.cookie}`;
	const parts = value.split(`; ${cookieName}=`);
	
	if (parts.length > 1) {
		/* ### Note ### */
		// array.pop() return "last element of index" and then remove on original array object
		// array.shift() return "first element of index" and then remove on original array object
		
		document.querySelector("input[name=userId]").value = parts.pop().split(";").shift();
		document.querySelector("input[name=remember]").checked = true;
	}
}
```
[Ref.] https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/pop  
[Ref.] https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/shift  
[Ref.] https://stackoverflow.com/questions/10730362/get-cookie-by-name  

###### delete cookie  
```js
function deleteCookie() {
	const cookieName = "something";
	const expireDate = "Thu, 01 Jan 1970 00:00:00 GMT";
	document.cookie = `${cookieName}=; expires=${expireDate};`;
}
```
