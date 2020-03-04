// only one checked in input type checkbox
```js
function onlyOneChecked(node){
	
	const status = node.checked;
	
	document.querySelectorAll("input[type=checkbox]:checked").forEach(item => {
		item.checked = false;
	});
	
	node.checked = status;
}
```
