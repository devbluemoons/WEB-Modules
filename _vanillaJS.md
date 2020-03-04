###### only one checked in input type checkbox
```js
function onlyOneChecked(data){
	
	document.querySelectorAll("input[type=checkbox]:checked").forEach(item => {
		item.checked = false;
	});
	data.checked = true;
}
```
