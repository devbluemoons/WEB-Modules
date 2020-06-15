###### how to use
```js
function howToUse(data) {
	
	const formData = new FormData();
	formData.append("data001", data.data001);
	formData.append("data002", data.data002);
	formData.append("data003", data.data003);
	
	fetch("/url-address", {
		method: "POST", // GET, POST, PUT, DELETE 
		body: formData  // data
	}).then(response => {
		if(!response.ok){
			throw Error(response.status);
		}
    		// return response.json();
    		// return response.text();
	}).then(data => {
		if(data) {
      			console.log(data);
    		}
	}).catch(error => {
		console.log("Error:",error);
	});
}
```
```java
@PostMapping("/registerDiRule")
@ResponseBody public String registerDiRule(@RequestParam Map<String, Object> param) throws Exception {
	try {
		service.registerDiRule(param);
	} catch (Exception e) {
		return e.getMessage();
	}
	return "";
}

// [INSERT] process에서 return 타입이 void가 아닌 string인 이유는 
// fetch 에서 [처리상태]를 [response] 결과로 return 받아야 하기 때문이다
// 실제로 return 받아야 할 data는 없지만 @ResponseBody를 선언함으로 [처리상태]를 [response]로 받는다 
```
