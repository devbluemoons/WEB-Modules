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
		<!-- content -->
		<!-- content -->
	</div>
</div>
```
  
```css
.modal {
	display: none;
	opacity: 0;
	transition: opacity: 500ms; 
}

.modal.is-visible {
	display: block;
	opacity: 1;
	
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

/** fade effect **/
@-webkit-keyframes fadein {
	0%   {opacity: 0;}
	100% {opacity: 1;}
}
@keyframes fadein {
	0%   {opacity: 0;}
	100% {opacity: 1;}
}
.fadeIn {
	-moz-animation   : fadein 0.5s linear;
	-webkit-animation: fadein 0.5s linear;
	animation        : fadein 0.5s linear;
}

@-webkit-keyframes fadeout {
	0%   {opacity: 1;}
	100% {opacity: 0;}
}
@keyframes fadeout {
	0%   {opacity: 1;}
	100% {opacity: 0;}
}
.fadeOut {
	-moz-animation     : fadeout 0.5s linear;
	-webkit-animation  : fadeout 0.5s linear;
	animation          : fadeout 0.5s linear;
}
```
  
```js
function bindingModal() {
	
	const modal = document.querySelector(".modal");
	const overlay = document.querySelector(".modal_overlay");
	const openBtn = document.getElementById("openPopup");
	const closeBtn = document.getElementById("closePopup");
	const b_close = document.querySelector(".b-close");
	
	function openModal() {
		modal.classList.remove("fadeOut");
		modal.classList.add("is-visible", "fadeIn");
	}
	
	// !!! 이 부분은 순서가 중요
	// 1) 먼저 fadeOut을 통해 클래스 애니메이션 효과를 적용
	// 2) 절대 fadeOut 코드와 같이 적용해서는 안된다 / 논리적인 오류 발생
	// 3) animation 효과가 적용된 element에 EventListener를 적용
	// 4) animationend 속성은 element의 animation 적용 시간이 끝나는 시점을 반환
	// 5) EventListener의 첫번째 인자로 animationend 속성을 적용
	// 6) 두번째 인자로 적용할 인자를 callback 함수 형태로 정의
	function closeModal() {
		modal.classList.add("fadeOut");
		modal.addEventListener("animationend", () => {
			modal.classList.remove("is-visible","fadeIn");
		}, {once: true});
	}
	
	openBtn.addEventListener("click", openModal);
	closeBtn.addEventListener("click", closeModal);
	b_close.addEventListener("click", closeModal);
	overlay.addEventListener("click", closeModal);
	
	/* escape */
	document.addEventListener("keydown", e => {
		e.keyCode === 27 ? closeModal() : null;
	});
}
```
