## closure
###### basic structure
```js
function closure() {
	let toggle = true;
	let count = 0;
	
	function innerFunc() {
		console.log(toggle, count);
    		toggle = !toggle;
    		count++;
	}
	return innerFunc;
}

const test = closure();

test(); // true 0
test(); // false 1
test(); // true 2 
```
###### self-invoking function
```js
// this function is called only once when page load
const closure = (function() {

    const greeting = "hello world!"
    
    return function() {
        console.log(greeting);
    }
})();

closure(); // hello world!
```
```js
// same code above anonymous function
function greeting() {

    const greeting = "hello world!"
    
    return function() {
        console.log(greeting);
    }
}

const closure = greeting();
closure(); // hello world!
```
###### free-variable
  
###### capture
  
  
  
[Ref.] https://offbyone.tistory.com/135
