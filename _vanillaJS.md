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
  
###### modal control 
```html
<div class="modal hidden">
	<div class="modal_overlay"></div>
	<div class="modal_content">
		<div class="b-close">X</div>
		<div class="btnRight">
			<a href="#">search</a>
			<a href="#">save</a>
			<a href="#" id="closePopup">close</a>
		</div>
		<!-- content -->	
	</div>
</div>
```
  
```css
.modal {
	position: fixed;
	top: 0;
	left: 0;
	width: 100%;
	height: 100%;
	display: flex;
	justify-content: center;
	align-items: center;
}
.modal_overlay {
	background-color: rgba(0, 0, 0, 0.7);
	width: 100%;
	height: 100%;
	position: absolute;
}
.b-close {
	position:absolute;
	top:15px; 
	right:15px; 
	width:21px; 
	height:21px;  
	cursor:pointer;
	text-indent:100000em;  
	background:url(../images/common/icon_close.gif) no-repeat;
}
.modal_content {
	background: white;
	padding:0; 
	position: absolute;
	width:900px;
	height:600px; 
	border:1px solid #cccccc;
	margin:0;  
	padding:25px; 
	z-index:500; 
}
.hidden {
	display: none;
}
```
  
```js
function bindingModal() {
	
	const modal = document.querySelector(".modal");
	const overlay = document.querySelector(".modal_overlay");
	const openBtn = document.getElementById("openPopup");
	const closeBtn = document.getElementById("closePopup");
	const b_close = document.querySelector(".b-close");
	
	const openModal = () => {
		modal.classList.remove("hidden");
	}
	const closeModal = () => {
		modal.classList.add("hidden");
	}
	
	openBtn.addEventListener("click", openModal);
	closeBtn.addEventListener("click", closeModal);
	b_close.addEventListener("click", closeModal);
	overlay.addEventListener("click", closeModal);
}
```
