
###### auto logout
```js
window.addEventListener("DOMContentLoaded", function() {
	// session invalid listener
	document.addEventListener("click", loadSessionTimeout);
	document.addEventListener("keydown", loadSessionTimeout);
	
	// this run, when index page load
	loadSessionTimeout();
});

// set session timeout option
function loadSessionTimeout() {
	resetTimer(() => {
		alert("세션이 만료 되었습니다.\n로그인 페이지로 이동합니다.");
		location.href = "/logout";
	}, 1000*60*30); // 로그인 세션 지속시간 : 30분
}
const resetTimer = (function() {
	let timer = null;
	return (func, ms) => {
		timer ? clearTimeout(timer) : null;
		timer = setTimeout(func, ms);
	}
})();
```
