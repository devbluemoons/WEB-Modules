#### data and time utilities
```js
//date class
class dateSingleTon{
	
	constructor() {
		this.date = new Date();
	}
	
	instance() {
		return {
			year: this.date.getFullYear(),
			month: this.date.getMonth(),
			day: this.date.getDay(),
			hours: this.date.getHours(),
			minutes: this.date.getMinutes(),
			seconds: this.date.getSeconds()
		}
	}
}

const date = new dateSingleTon().instance();

//getFullYear
function getYear(){
	return date.year;
}

//getMonth
function getMonth(){
	return parseInt(date.month) < 10 ? `0${date.month}` : date.month;
}

//getDay
function getDay(){
	return parseInt(date.day) < 10 ? `0${date.day}` : date.day;
}

//getHours
function getHours(){
	return parseInt(date.hours) < 10 ? `0${date.hours}` : date.hours;
}

//getMinutes
function getMinutes(){
	return parseInt(date.minutes) < 10 ? `0${date.minutes}` : date.minutes;
}

//getSeconds
function getSeconds(){
	return parseInt(date.seconds) < 10 ? `0${date.seconds}` : date.seconds;
}


//getYYYYMMDD
function yyyyMMdd() {
	
	const yyyy = date.year();
	const mm = parseInt(date.month) < 10 ? `0${date.month}` : date.month;
	const dd = parseInt(date.day) < 10 ? `0${date.day}` : date.day;
	
	return `${yyyy}-${mm}-${dd}`;
}

//getHHMMSS
function hhMMss() {
	
	const hh = parseInt(date.hours) < 10 ? `0${date.hours}` : date.hours;
	const mm = parseInt(date.minutes) < 10 ? `0${date.minutes}` : date.minutes;
	const ss = parseInt(date.seconds) < 10 ? `0${date.seconds}` : date.seconds;
	
	return `${hh}:${mm}:${ss}`;
}

//getCurrentTime
function getCurrentTime() {
	return `${yyyyMMdd()} ${hhMMss()}`;
}
```
