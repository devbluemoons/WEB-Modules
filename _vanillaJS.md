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
	
	const openBtn = document.getElementById("openPopup");
	const closeBtn = document.getElementById("closePopup");
	const closeIcon = document.querySelector(".close_icon");
	const overlay = document.querySelector(".modal_overlay");
	
	openBtn.addEventListener("click", openModal);
	closeBtn.addEventListener("click", closeModal);
	closeIcon.addEventListener("click", closeModal);
	overlay.addEventListener("click", closeModal);
	
	/* escape */
	document.addEventListener("keydown", e => {
		e.keyCode === 27 ? closeModal() : null;
	});
}

function openModal() {
	const modal = document.querySelector(".modal");
	
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
	const modal = document.querySelector(".modal");
	
	modal.classList.add("fadeOut");
	modal.addEventListener("animationend", () => {
		modal.classList.remove("is_visible", "fadeIn");
	}, {once: true});
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
	
	/* !!주의 : form 데이터를 넘길때  get 메소드를 사용하면 typeError가 발생한다
	404 같은 bad request 의 경우, catch() 에서 처리되는 거 아닌가? 라고 생각 하실 수 있겠지만 
	google develop 의 document 에 따르면 request 가 완료되지 않은 경우
	(통신이 끊기거나 시간이 경과된 경우) 에만 catch() 메소드를 통해 처리된다. */
	
	fetch("/test/findAllTestDev", {
		method: "POST",
		body: new FormData(document.getElementById("searchForm"))
	}).then(response => {
		if(!response.ok) {
			throw Error(response.status);
		}
		return response.text();
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
// you must set same name key and param
formData.append("key", value);
const seq = formData.get("SEQ").trim();
formData.delete("SEQ");
formData.has("SEQ");

const formData = new FormData(document.getElementById("searchForm"));
```
  
###### reset form tag data
```js
document.getElementById("myForm").reset();
```
  
###### search formData's key / value
```js
const formData = new FormData();
formData.append("key", value);

for(let entry of formData.entries()) {
    console.log(entry);
}
```
https://stackoverflow.com/questions/40062477/formdata-append-not-working
  
###### document.querySelector / element.querySelector
```js
document.querySelector("#updateForm input[name=address]");
const el = document.getElementById("deleteForm");
const seq = el.querySelector("input[type=hidden]").value;
const radio = el.querySelector("input[type=radio]:checked");
const trs = el.querySelectorAll("tbody tr");

el.querySelector("input[name=MODEL]").value = typeof data[0].MODEL === "undefined" ? "" : data[0].MODEL;
el.querySelector("select[name=FORMAT_ID]").value = data[0].FORMAT_ID;
el.querySelector("input[name=HC_YN]").checked = data[0].HC_YN === "Y" ? true : false;
```
  
###### setInterval with clearInterval
```js
function intervalSearch() {
	
	const oneMinute = 60 * 1000;
	const cycle = document.getElementById("cycle");
	const time = parseInt(cycle.value) * oneMinute;
	localStorage.setItem("cycle", cycle.value);
	
	//함수 호출 주기보다  내부 로직 실행속도가 더 오래 걸릴 경우 문제가 발생하므로 주의하여 사용
	clearInterval(Object.prototype.timer);
	Object.prototype.timer = setInterval(() => {
		location.href = "";
	}, time);
}
```
###### table sort
```html
<th class="sorting" onclick="sort(event)"><input type="hidden" value="001"/>001</th>
```
  
```js
function sort(e){
	
	let className = null;
	
	if(e.target.classList.length === 1){
		className = "sortingDown";
	}else if(e.target.classList.contains("sortingDown")){
		className = "sortingUp";
	}else if(e.target.classList.contains("sortingUp")){
		className = "sortingDown";
	}
	
	const ths = document.getElementsByTagName("th");
	
	for(let i=0; i<ths.length; i++){
		ths[i].classList.remove("sortingUp","sortingDown");
	}
	e.target.classList.add(className);
	
	const el = document.getElementsByClassName(className);
	const orderBy = el[0].querySelector("input[type=hidden]").value;
	const sortKey = className === "sortingDown" ? "DESC" : "ASC";
	
	const param = {orderBy : orderBy, sortKey : sortKey};
	findData(param);
}
```
  
###### confirm
```js
const yn = confirm("confirm method returns boolean value when you click yes or no");
if(!yn) return;
```
  
###### check form values
```js
function checkID(value) {
	// 8~12자 이내 영문, 숫자 ,특수문자 포함한 비밀번호 조합
	const english = value.search(/[a-z]/ig);
	const korean = /[ㄱ-ㅎ|ㅏ-ㅣ|가-힣]/;

	if(value.length < 4 || value.length > 20){
		alert("[ID]는 4자리 ~ 20자리 이내로 입력해 주세요.");
		return false;
	}
	if(value.search(/₩s/) != -1){
		alert("[ID]는 공백없이 입력해 주세요.");
		return false;
	} 
	if(english < 0){
		alert("영문(소문자)를 포함하여 [ID]를 작성해 주세요.");
		return false;
	}
	if(value.match(korean)){
		alert("한글은 [ID]에 포함될 수 없습니다.");
		return false;
	}
	return true;
}

function checkPassWord(value) {
	// 8~20자 이내 영문(소문자), 숫자 ,특수문자 포함한 비밀번호 조합
	// input[type=password] 는 키보드 설정이 한글이어도 영문으로 입력받도록 설정되어 있다
	
	const number = value.search(/[0-9]/g);
	const english = value.search(/[a-z]/ig);
	const specialCharacter = value.search(/[`~!@@#$%^&*|₩₩₩'₩";:₩/?]/gi);

	if(value.length < 8 || value.length > 20){
		alert("[비밀번호]는 8자리 ~ 20자리 이내로 입력해 주세요.");
		return false;
	}
	if(value.search(/₩s/) != -1){
		alert("[비밀번호]는 공백없이 입력해 주세요.");
		return false;
	} 
	if(number < 0 || english < 0 || specialCharacter < 0 ){
		alert("[비밀번호]는 영문(소문자), 숫자, 특수문자를 혼합하여 입력해 주세요.");
		return false;
	}
	return true;
}

function checkKorean(value) {
	const regExp = /[ㄱ-ㅎ|ㅏ-ㅣ|가-힣]/;
	if(!value.match(regExp)){
		alert("[이름]은 한글로만 작성할 수 있습니다.");
		return false;
	}
	return true;
}

function verifyEmail(value) {
	const regExp = /^[0-9a-zA-Z]([-_.]?[0-9a-zA-Z])*@[0-9a-zA-Z]([-_.]?[0-9a-zA-Z])*.[a-zA-Z]{2,3}$/i;
	if(!value.match(regExp)){
		alert("@문자와 .(dot)문자를 포함하여 [이메일] 형식에 맞게 작성하세요.");
		return false;
	}
	return true;
};
```
  
###### formatting by RegExp
```js
//formatting only english with number
document.querySelector("input[name=USER_ID]").addEventListener("keyup", function(e) {
	e.target.value = e.target.value.replace(/[^a-z|0-9]/gi,"");
});
```
  
```js
<!-- only korean -->
document.querySelector("input[name=USER_NAME]").addEventListener("keyup", function(e) {
	e.target.value = e.target.value.replace(/[^ㄱ-ㅎ|ㅏ-ㅣ|가-힣]/gi,"");
});
```
  
```js
<!-- only number with hyphen -->
document.querySelector("input[name=PHONE]").addEventListener("keyup", function(e){
	e.target.value = e.target.value.replace(/[^0-9]/gi,"");
	e.target.value = e.target.value.replace(/(\d{3})(\d{4})(\d{4})/, "$1-$2-$3");
});
```
[Ref.] https://stackoverflow.com/questions/6981487/insert-hyphens-in-javascript
  
###### set text to li tag
```js
const li = document.createElement("li");
li.textContent = "abc123";
```
  
###### real time search using input and div tag
```html
<input type="text" class="input04 wdt160px" name="DIRECT_INPUT" placeholder="직접입력" disabled>
<div id="searchResult" class="real_time_search wdt160px"></div>
```
```css
.show {
	display: block;
	position: fixed;
	max-height: 250px;
	overflow: auto;
	border: solid 1px #EBEBE4;
	box-sizing: border-box;
	background-color: #FFFFFF;
}
.real_time_search li {
	padding-left: 3px;
	padding-bottom: 3px;
}
.real_time_search li:hover {
	background-color: #EBEBE4;
}
```
```js
// 실시간 검색(자동완성)
document.querySelector("input[name=DIRECT_INPUT]").addEventListener("keyup", e => {

	if(e.keyCode === 27) return false; // when click escape button
	const value = e.target.value || "";
	
	delayKeyup(function() {
		
		const formData = new FormData();
		formData.append("IP_STR", value);
		
		fetch("/ip/findDiIpByIpStr", {
			method: "POST",
			body: formData
		}).then(response => {
			if(!response.ok){
				throw Error(response.status);
			}
			return response.json();
		}).then(data => {
			if(data) {
				realTimeSearch(data);
			}
		}).catch(error => {
			console.log("Error:",error);
		});
		
	}, 500);
});

function realTimeSearch(data) {
	
	const searchKeyword = document.querySelector("input[name=DIRECT_INPUT]");
	const searchResult = document.getElementById("searchResult");
	
	if(searchKeyword.value !== "") {
		searchResult.innerHTML = "";
		searchResult.classList.add("show");
	}else{
		searchResult.classList.remove("show");
	}
	
	const ul = document.createElement("ul");
	data.forEach(item => {
		const li = document.createElement("li");
		li.textContent = item.IP_STR;
		li.addEventListener("click", e => {
			searchKeyword.value = e.target.textContent;
			searchResult.classList.remove("show");
		});
		ul.appendChild(li);
	});
	searchResult.append(ul);
}

document.querySelector("body").addEventListener("click", () => {
	document.getElementById("searchResult").classList.remove("show");
});
document.addEventListener("keydown", e => {
	if(e.keyCode === 27) {
		document.getElementById("searchResult").classList.remove("show");
	}
});
```
###### delay (basic)
```js
function delay(callback, ms) {
	let timer = 0;
	
	return function() {
		const self = this;
		const args = arguments;
		
		clearTimeout(timer);
		
		timer = setTimeout(() => {
			callback.apply(self, args);
		}, ms || 0);
	};
}
```
###### delay (es6)
```js
function delayES6(fn, ms) {

	let timer = 0;
	const self = this;
	
	return (...args) => {
		clearTimeout(timer);
		timer = setTimeout(fn.bind(self, ...args), ms || 0);
	}
}
```
###### delay (closure)
```js
const delayKeyup = (function() {
	let timer = null;
	return (func, ms) => {
		timer ? clearTimeout(timer) : null;
		timer = setTimeout(func, ms);
	}
})();
```
[Ref.01] https://stackoverflow.com/questions/1909441/how-to-delay-the-keyup-handler-until-the-user-stops-typing  
[Ref.02] https://c10106.tistory.com/4274  
  
###### how to get object keys
```js
const obj = {
	aaa: 111,
	bbb: 222,
	ccc: 333
}

const keys = Object.keys(obj);

keys.forEach(item => {
	console.log(obj[item]);
});
```
  
###### contains / add / remove
```js
if(element.classList.contains("active")) {
    element.classList.remove("active");
}else {
    document.querySelectorAll(".treeview").forEach(item => item.classList.remove("active"));
    element.classList.add("active");
}
```
  
###### throw new Error();
```js
const errorMessage = "Thie is a Error";

arrData.forEach(item => {
    if(parseInt(item) > 255) {
        throw new Error(errorMessage);
    }
});
```
  
###### filtering by ip address rule
```js
// filtering ip
const ipArr = "010.011.017.019".trim().split(".");
const ipIntArr = [...ipArr].map(item => parseInt(item));

console.log(ipIntArr.join(".")); // 10.11.17.19
```
  
###### getAttribute
```html
<div class="btn_blue" th:value="${row.SEQ}">Action</div>
```
```js
function selectRow(e) {
    console.log(e.target.getAttribute("value"));
}
```
###### localStorage
```js
//setItem
localStorage.setItem('myCat', 'Tom');
//getItem
var cat = localStorage.getItem('myCat');
//removeItem
localStorage.removeItem('myCat');
//clear (all items)
localStorage.clear();
```
