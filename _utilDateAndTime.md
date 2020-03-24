#### data and time utilities
```js
//date class
class CurrentDate{
	
	constructor() {
		this.date = new Date();
	}
	
	instance() {
		return {
			year   : this.date.getFullYear(),
			month  : this.date.getMonth(),
			date   : this.date.getDate(),
			hours  : this.date.getHours(),
			minutes: this.date.getMinutes(),
			seconds: this.date.getSeconds(),
		}
	}
}

const date = new CurrentDate().instance();

//getFullYear
function getYear() {
	return date.year;
}

//getMonth
function getMonth() {
	return (date.month + 1) < 10 ? `0${date.month + 1}` : (date.month + 1);
}

//getDay
function getDay() {
	return date.date < 10 ? `0${date.date}` : date.date;
}

//getHours
function getHours() {
	return date.hours < 10 ? `0${date.hours}` : date.hours;
}

//getMinutes
function getMinutes() {
	return date.minutes < 10 ? `0${date.minutes}` : date.minutes;
}

//getSeconds
function getSeconds() {
	return date.seconds < 10 ? `0${date.seconds}` : date.seconds;
}

//getYYYYMMDD
function getYyyyMmDd() {
	
	const yyyy = date.year;
	const mm = (date.month + 1) < 10 ? `0${date.month + 1}` : (date.month + 1);
	const dd = date.date < 10 ? `0${date.date}` : date.date;
	
	return `${yyyy}-${mm}-${dd}`;
}

//getHHMMSS
function getHhMMss() {
	
	const hh = date.hours < 10 ? `0${date.hours}` : date.hours;
	const mm = date.minutes < 10 ? `0${date.minutes}` : date.minutes;
	const ss = date.seconds < 10 ? `0${date.seconds}` : date.seconds;
	
	return `${hh}:${mm}:${ss}`;
}

//getCurrentTime
function getCurrentTime() {
	return `${yyyyMMdd()} ${hhMMss()}`;
}

//first day of this month
function getFirstDay() {
	
	const firstDay = new Date(date.year, date.month, 1);
	
	let yyyy = firstDay.getFullYear();
	let mm = firstDay.getMonth() + 1;
	let dd = firstDay.getDate();
	
	mm = (mm < 10) ? `0${mm}` : mm;
	dd = dd < 10 ? `0${dd}` : dd;
	
	return `${yyyy}-${mm}-${dd}`;
}

//first day of last month
function getLastMonthFirstDay() {
	
	const firstDay = new Date(date.year, date.month, 1);
	
	let yyyy = firstDay.getFullYear();
	let mm = firstDay.getMonth();
	let dd = firstDay.getDate();
	
	mm = (mm < 10) ? `0${mm}` : mm;
	dd = dd < 10 ? `0${dd}` : dd;
	
	return `${yyyy}-${mm}-${dd}`;
}

//last day of last month
function getLastMonthLastDay() {
	
	const firstDay = new Date(date.year, (date.month + 1), 0);
	
	let yyyy = firstDay.getFullYear();
	let mm = firstDay.getMonth();
	let dd = firstDay.getDate();
	
	mm = (mm < 10) ? `0${mm}` : mm;
	dd = dd < 10 ? `0${dd}` : dd;
	
	return `${yyyy}-${mm}-${dd}`;
}
```
