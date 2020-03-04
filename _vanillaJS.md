###### only one checked in input type checkbox
```html
<input type="checkbox" value="01" onclick="onlyOneChecked(event)">
```

```js
function onlyOneChecked(e){
	
	const status = e.target.checked;
	
	document.querySelectorAll("input[type=checkbox]:checked").forEach(item => {
		item.checked = false;
	});
	
	e.target.checked = status;
}
```
  
###### get selected option value from select tag
```html
<select class="seltype01" onchange="selectedOption(event)">
	<option value="01">JavaScript</option>
	<option value="02">NodeJS</option>
	<option value="03">MongoDB</option>
</select>
```
  
```js
function selectedOption(event)(e){
	console.log(e.target.value);
}
```
  
###### hide bootstrap modal 
https://stackoverflow.com/questions/46577690/hide-bootstrap-modal-using-pure-javascript-on-click/52570205
