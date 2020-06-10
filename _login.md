
###### auto logout
```js
// session invalid listener
function sessionInvalidTimer() {
	setTimeout(() => {
		alert("This session is expired.\nIt will move login page.");
		location.href = "/logout";
	}, 1000*60);
}
function resetTimer() {
	let timer = null;
	return () => {
		timer ? clearTimeout(timer) : null;
		timer = sessionInvalidTimer();
	}
}
document.addEventListener("click", resetTimer);
```
