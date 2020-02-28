#### data and time utilities
```js

/*getFullYear*/
function getYear(){
	return new Date().getFullYear();
}

/*getMonth*/
function getMonth(){
	const date = new Date();
	return parseInt(date.getMonth()) < 10 ? `0${date.getMonth()}` : date.getMonth();
}

/*getDate*/
function getDay(){
	const date = new Date();
	return parseInt(date.getDay()) < 10 ? `0${date.getDay()}` : date.getDay();
}

/*getHours*/
function getHours(){
	const date = new Date();
	return parseInt(date.getHours()) < 10 ? `0${date.getHours()}` : date.getHours();
}

/*getMinutes*/
function getMinutes(){
	const date = new Date();
	return parseInt(date.getMinutes()) < 10 ? `0${date.getMinutes()}` : date.getMinutes();
}

/*getSeconds*/
function getSeconds(){
	const date = new Date();
	return parseInt(date.getSeconds()) < 10 ? `0${date.getSeconds()}` : date.getSeconds();
}


/*getYYYYMMDD*/
function yyyyMMdd() {
	const date = new Date();
	
	const yyyy = date.getFullYear();
	const mm = parseInt(date.getMonth()) < 10 ? `0${date.getMonth()}` : date.getMonth();
	const dd = parseInt(date.getDay()) < 10 ? `0${date.getDay()}` : date.getDay();
	
	return `${yyyy}-${mm}-${dd}`;
}

/*getHHMMSS*/
function hhMMss() {
	const date = new Date();
	
	const hh = parseInt(date.getHours()) < 10 ? `0${date.getHours()}` : date.getHours();
	const mm = parseInt(date.getMinutes()) < 10 ? `0${date.getMinutes()}` : date.getMinutes();
	const ss = parseInt(date.getSeconds()) < 10 ? `0${date.getSeconds()}` : date.getSeconds();
	
	return `${hh}:${mm}:${ss}`;
}

/*getCurrentTime*/
function getCurrentTime() {
	return `${yyyyMMdd()} ${hhMMss()}`;
}


```
