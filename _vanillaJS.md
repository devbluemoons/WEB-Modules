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
<select onchange="selectedOption(event)">
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
<div class="modal">
	<div class="modal_overlay"></div>
	<div class="modal_content">
		<div class="close_icon">X</div>
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
}

.modal.is_visible {
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
.close_icon {
	position: absolute;
	top: 15px;
	right: 15px;
	width: 21px;
	height: 21px;
	cursor: pointer;
	text-indent: 100000em;
	background: url(../images/common/icon_close.gif) no-repeat;
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
@-webkit-keyframes fade-in {
	0%   {opacity: 0;}
	100% {opacity: 1;}
}
@keyframes fade-in {
	0%   {opacity: 0;}
	100% {opacity: 1;}
}
.fadeIn {
	-moz-animation   : fade-in 700ms;
	-webkit-animation: fade-in 700ms;
	animation        : fade-in 700ms;
}

@-webkit-keyframes fade-out {
	0%   {opacity: 1;}
	100% {opacity: 0;}
}
@keyframes fade-out {
	0%   {opacity: 1;}
	100% {opacity: 0;}
}
.fadeOut {
	-moz-animation   : fade-out 700ms;
	-webkit-animation: fade-out 700ms;
	animation        : fade-out 700ms;
}
```
  
```js
function bindingModal() {
	
	const modal = document.querySelector(".modal");
	const overlay = document.querySelector(".modal_overlay");
	const openBtn = document.getElementById("openPopup");
	const closeBtn = document.getElementById("closePopup");
	const closeIcon = document.querySelector(".close_icon");
	
	function openModal() {
		modal.classList.remove("fadeOut");
		modal.classList.add("is_visible", "fadeIn");
	}
	
	// !!! 이 부분은 순서가 중요
	// 1) 먼저 fadeOut을 통해 클래스 애니메이션 효과를 적용
	// 2) 절대 fadeOut 코드와 같이 적용해서는 안된다 / 논리적인 오류 발생
	// 3) animation 효과가 적용된 element에 EventListener를 추가
	// 4) animationend 속성은 element의 animation 적용 시간이 끝나는 시점을 반환
	// 5) EventListener의 첫번째 parameter로 animationend 속성을 적용
	// 5) 두번째 parameter는 첫번째 parameter가 리턴되는 시점부터 함수를 실행
	// 6) 두번째 parameter를 callback 함수 형태로 정의
	// 7) 세번째 parameter로 {once:true} 를 object 형태로 적용
	// 8) 세번째 parameter로 인하여 EventListener는 한번만 실행된다
	
	function closeModal() {
		modal.classList.add("fadeOut");
		modal.addEventListener("animationend", () => {
			modal.classList.remove("is_visible", "fadeIn");
		}, {once: true});
	}
	
	openBtn.addEventListener("click", openModal);
	closeBtn.addEventListener("click", closeModal);
	closeIcon.addEventListener("click", closeModal);
	overlay.addEventListener("click", closeModal);
	
	/* escape */
	document.addEventListener("keydown", e => {
		e.keyCode === 27 ? closeModal() : null;
	});
}
```
  
###### xmlHttpRequest
```js
function xmlHttpRequest(type, url, data){
	
	return new Promise((resolve, reject) => {
		
		const xhr = new XMLHttpRequest();
		
		xhr.open(type, url, true);
		xhr.onreadystatechange = () => {
			
			if (xhr.readyState !== XMLHttpRequest.DONE) return;
			if (xhr.status >= 200 && xhr.status < 300) {
				resolve(xhr.response);
			} else {
				reject({
					status: xhr.status,
					statusText: xhr.statusText
				});
			}
		};
		xhr.send(data ? JSON.stringify(data) : null);
	});
}
```

###### fetch
```js
function search() {
	
	/* !!주의 : form 데이터를 넘길때  get 메소드를 사용하면 typeError가 발생한다 */
	
	fetch("/test/findAllTestDev", {
		method: "POST",
		body: new FormData(document.getElementById("searchForm"))
	}).then(response => {
		if(response.ok) {
			return response.text();
		}
	}).then(data => {
		document.getElementById("tableContents").innerHTML = data;
	}).catch(error => {
		console.log("error", error);
	});
}
```
  
###### search by keydown enter
```js
function searchByEnter() {
	document.addEventListener("keydown", e => {
		e.keyCode === 13 ? search() : null;
	});
}
```
  
###### formData
```js
const formData = new FormData();
formData.append("key", value);

const formData = new FormData(document.getElementById("searchForm");
```
  
###### reset form tag data
```js
document.getElementById("myForm").reset();
```
  
###### document.querySelector / element.querySelector
```js
document.querySelector("#updateForm input[name=address]");
const el = document.getElementById("deleteForm");
const seq = el.querySelector("input[type=hidden]").value;
```
