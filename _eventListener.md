###### binding `element` or `node`
```js
document.querySelector("body").addEventListener("click", () => {});
document.removeEventListener("keydown", focusTarget);
document.addEventListener("keydown", focusTarget);

function focusTarget(e) {
	
	const el = document.querySelector("#searchResult > ul");
	const focus = el.querySelector(".focus");
	//enter
	if(e.keyCode === 13) {
		if(focus) {
			document.querySelector("input[name=DIRECT_INPUT]").value = focus.textContent;
			document.getElementById("searchResult").classList.remove("show");
			focus.classList.remove("focus");
		}
	}
	//escape
	if(e.keyCode === 27) {
		document.getElementById("searchResult").classList.remove("show");
		focus ? focus.classList.remove("focus") : null;
	}
	//up
	if(e.keyCode === 38) {
		if(focus) {
			focus.classList.remove("focus");
			if(!focus.previousElementSibling) {
				el.lastElementChild.classList.add("focus");
				return
			}
			focus.previousElementSibling.classList.add("focus");
		}else {
			el.lastElementChild.classList.add("focus");
		}
	}
	//down
	if(e.keyCode === 40) {
		if(focus) {
			focus.classList.remove("focus");
			if(!focus.nextElementSibling) {
				el.firstElementChild.classList.add("focus");
				return
			}
			focus.nextElementSibling.classList.add("focus");
		}else {
			el.firstElementChild.classList.add("focus");
		}
	}
}
```
  
- 이벤트리스너를 추가하고 제거하는 시점을 명확하게 정하는 것이 좋다
- 이벤트에 바인딩 할 함수는 익명함수를 사용해도 되지만 외부함수 정의하고 대입하는 것이 더 명확하다
