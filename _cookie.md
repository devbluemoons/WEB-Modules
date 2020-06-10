###### set cookie
  
###### get cookie  
```js
function autocompleteUserId() {
	
	const cookieName = "userId";
	const value = `; ${document.cookie}`;
	const parts = value.split(`; ${cookieName}=`);
	
	if (parts.length === 3) {
		document.querySelector("input[name=userId]").value = parts.pop().split(';').shift();
		document.querySelector("input[name=remember]").checked = true;
	}
}
```
[Ref.] https://stackoverflow.com/questions/10730362/get-cookie-by-name  

###### delete cookie  
  
