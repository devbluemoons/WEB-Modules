## Real Time Search
```html
<input autocomplete="off" type="text" name="DIRECT_INPUT" placeholder="direct input">
<div id="searchResult" class="real_time_search"></div>
```
```css
.real_time_search {
	display: none;
}
.show {
	display: block;
	position: fixed;
	max-height: 250px;
	overflow: auto;
	border: solid 1px #2986B8;
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
	/* except : enter, escape, up, down */
	if(e.keyCode === 13 || e.keyCode === 27 || e.keyCode === 38 || e.keyCode === 40) return false;
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
		
	}, 300);
});

// self-variable function
const delayKeyup = (function() {
	let timer = null;
	return (func, ms) => {
		timer ? clearTimeout(timer) : null;
		timer = setTimeout(func, ms);
	}
})(); // this function is called only once when page load 

function realTimeSearch(data) {
	
	const searchKeyword = document.querySelector("input[name=DIRECT_INPUT]");
	const searchResult = document.getElementById("searchResult");
	
	searchResult.innerHTML = "";
	if(searchKeyword.value !== "") {
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
	bindingKeyCode();
}

function bindingKeyCode() {
	document.removeEventListener("keydown", focusTarget);
	document.addEventListener("keydown", focusTarget);
}

function focusTarget(e) {
	
	const box = document.getElementById("searchResult");
	const ul = document.querySelector("#searchResult > ul");
	const focus = ul.querySelector(".focus");
	//enter
	if(e.keyCode === 13) {
		if(focus) {
			document.querySelector("input[name=DIRECT_INPUT]").value = focus.textContent;
			document.getElementById("searchResult").classList.remove("show");
		}
	}
	//escape
	if(e.keyCode === 27) {
		document.getElementById("searchResult").classList.remove("show");
	}
	//up
	if(e.keyCode === 38) {
		if(focus) {
			focus.classList.remove("focus");
			if(!focus.previousElementSibling) {
				ul.lastElementChild.classList.add("focus");
				box.scrollTop = box.scrollHeight - box.offsetHeight;
				return
			}
			focus.previousElementSibling.classList.add("focus");
			if(focus.offsetTop <= box.scrollTop) {
				box.scrollTop -= focus.offsetHeight;
			}
		}else {
			ul.lastElementChild.classList.add("focus");
			box.scrollTop = box.scrollHeight - box.offsetHeight;
		}
	}
	//down
	if(e.keyCode === 40) {
		if(focus) {
			focus.classList.remove("focus");
			if(!focus.nextElementSibling) {
				ul.firstElementChild.classList.add("focus");
				box.scrollTop = 0;
				return
			}
			focus.nextElementSibling.classList.add("focus");
			if(focus.offsetTop >= box.scrollTop + box.offsetHeight - focus.offsetHeight) {
				box.scrollTop += focus.offsetHeight;
			}
		}else {
			ul.firstElementChild.classList.add("focus");
		}
	}
}

document.querySelector("body").addEventListener("click", () => {
	document.getElementById("searchResult").classList.remove("show");
});
```
