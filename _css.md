###### how to set multiple css style
```js
const li = document.createElement("li");
const edit = `<i class='fa fa-fw fa-edit' style="color: dodgerblue;"></i>`;
const remove = `<i class='fa fa-trash-o' style="color: orangered"></i>`;

li.style.cssText = "min-width: 200px; display: flex; justify-content: space-between;";
```
[Ref.] https://stackoverflow.com/questions/3968593/how-can-i-set-multiple-css-styles-in-javascript  
  
###### placeholder vertical-align
```css
::placeholder {
	position: absolute;
	line-height: ?px;
}
```
