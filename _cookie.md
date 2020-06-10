###### set cookie
  
###### get cookie  
```js
function autocompleteUserId() {
	
	const cookieName = "userId";
	const value = `; ${document.cookie}`;
	const parts = value.split(`; ${cookieName}=`);
	
	if (parts.length > 1) {
		/* ### Note ### */
		// array.pop() return last of index and then remove on original array
		// array.shift(); return first of index and then remove on orginal array
		
		document.querySelector("input[name=userId]").value = parts.pop().split(';').shift();
		document.querySelector("input[name=remember]").checked = true;
	}
}
```
[Ref.] https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/pop  
[Ref.] https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/shift  
[Ref.] https://stackoverflow.com/questions/10730362/get-cookie-by-name  

###### delete cookie  
  
