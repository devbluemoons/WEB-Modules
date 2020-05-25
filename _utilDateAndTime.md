#### data and time utilities
```js
//date class
class CurrentDate {
	
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

//getFullYear
function getYear() {
	const date = new CurrentDate().instance();
	return date.year;
}

//getMonth
function getMonth() {
	const date = new CurrentDate().instance();
	return (date.month + 1) < 10 ? `0${date.month + 1}` : (date.month + 1);
}

//getDay
function getDay() {
	const date = new CurrentDate().instance();
	return date.date < 10 ? `0${date.date}` : date.date;
}

//getHours
function getHours() {
	const date = new CurrentDate().instance();
	return date.hours < 10 ? `0${date.hours}` : date.hours;
}

//getMinutes
function getMinutes() {
	const date = new CurrentDate().instance();
	return date.minutes < 10 ? `0${date.minutes}` : date.minutes;
}

//getSeconds
function getSeconds() {
	const date = new CurrentDate().instance();
	return date.seconds < 10 ? `0${date.seconds}` : date.seconds;
}

//getYYYYMMDD
function yyyyMMdd() {
	const date = new CurrentDate().instance();
	
	const yyyy = date.year;
	const mm = (date.month + 1) < 10 ? `0${date.month + 1}` : (date.month + 1);
	const dd = date.date < 10 ? `0${date.date}` : date.date;
	
	return `${yyyy}-${mm}-${dd}`;
}

//getHHMMSS
function HHmmss() {
	const date = new CurrentDate().instance();
	
	const hh = date.hours < 10 ? `0${date.hours}` : date.hours;
	const mm = date.minutes < 10 ? `0${date.minutes}` : date.minutes;
	const ss = date.seconds < 10 ? `0${date.seconds}` : date.seconds;
	
	return `${hh}:${mm}:${ss}`;
}

//getHHMM
function HHmm() {
	const date = new CurrentDate().instance();
	
	const hh = date.hours < 10 ? `0${date.hours}` : date.hours;
	const mm = date.minutes < 10 ? `0${date.minutes}` : date.minutes;
	
	return `${hh}:${mm}`;
}

//getYYYYMMDDHHmmss
function yyyyMMddHHmmss(baseDate) {
	const dateFmt = new Date(baseDate);
	
	const yyyy = dateFmt.getFullYear();
	const MM = (dateFmt.getMonth() + 1) < 10 ? `0${dateFmt.getMonth() + 1}` : (dateFmt.getMonth() + 1);
	const dd = dateFmt.getDate() < 10 ? `0${dateFmt.getDate()}` : dateFmt.getDate();
	
	const hh = dateFmt.getHours() < 10 ? `0${dateFmt.getHours()}` : dateFmt.getHours();
	const mm = dateFmt.getMinutes() < 10 ? `0${dateFmt.getMinutes()}` : dateFmt.getMinutes();
	const ss = dateFmt.getSeconds() < 10 ? `0${dateFmt.getSeconds()}` : dateFmt.getSeconds();
	
	return `${yyyy}-${MM}-${dd} ${hh}:${mm}:${ss}`;
}

//getCurrentTime
function getCurrentTime() {
	return `${yyyyMMdd()} ${HHmmss()}`;
}

//first day of this month
function getFirstDay() {
	const date = new CurrentDate().instance();
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
	const date = new CurrentDate().instance();
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
	const date = new CurrentDate().instance();
	const lastDay = new Date(date.year, (date.month + 1), 0);
	
	let yyyy = lastDay.getFullYear();
	let mm = lastDay.getMonth();
	let dd = lastDay.getDate();
	
	mm = (mm < 10) ? `0${mm}` : mm;
	dd = dd < 10 ? `0${dd}` : dd;
	
	return `${yyyy}-${mm}-${dd}`;
}

// 30 minutes ago from now
function get30minutesAgo() {
	const date = new Date();
	date.setMinutes(date.getMinutes() - 30);
	
	const hh = (date.getHours() < 10) ? `0${date.getHours()}` : date.getHours();
	const mm = (date.getMinutes() < 10) ? `0${date.date.getMinutes()}` : date.getMinutes();
	
	return `${yyyyMMdd()} ${hh}:${mm}`;
}
```
