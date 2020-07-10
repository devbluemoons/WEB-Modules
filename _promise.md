###### promise
```js
new Promise((resolve, reject) => {
    const status = 200;	
    resolve(status);
}).then(result => result === 200 ? console.log("status is 200!"); : null);
```  
###### async
```js
// 함수 앞에 붙여서 사용
async function asyncFunc(){
  //
}
```
###### await
```js
// [async] 키워드가 존재하는 함수 내에서 사용
async function asyncFunc(url){
  await fetch(url);
}
```
## 비동기 함수 순차적 병렬처리
```js
// [await] 키워드를 통해 [비동기 함수]의 처리가 완료될 때까지 대기할 수 있다
// 중요한 것은 [await] 키워드를 사용한 [비동기 함수]는 반드시 상태를 [return] 해야만 올바르게 작동한다

function insertData(data) {

  const formData = new FormData();
  formData.append("data", data);
  
  // 이 부분이 가장 중요한 [핵심 포인트] 이다
  // 비동기 함수인 fetch 앞에 [return] 키워드를 붙여줘야만 [await] 가 비동기 [처리상태]를 알 수 있다
  return fetch("/anyTable/insertData", {
		method: "POST",
		body: formData
	}).then(response => {
		if(!response.ok){
			throw Error(response.status);
		}
	}).catch(error => {
		console.log("Error:",error);
	});
}

function findData() {
  const url = "127.0.0.1";
  return fetch(url);
}

// 전혀 다른 비동기 함수들을 순차적으로 처리하는 예시
// 1. 파라미터로 받은 데이터 배열을 루프를 돌며 하나씩 꺼내서 비동기 함수의 인자로 대입하여 [순차적]으로 호출
// 2. 루프 바깥쪽 비동기 함수가 대기하고 있다가 루프가 종료되면 호출된다
(async function(dataArr) {
  for(const item of dataArr) {
    await insertData(item); /*1*/
  }
  findData(); /*2*/
})();
```
[Ref.] https://stackoverflow.com/questions/56348062/insert-in-for-each-with-async-await/56348449#56348449
