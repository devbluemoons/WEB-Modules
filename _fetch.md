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
