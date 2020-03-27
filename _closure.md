## closure
###### Basic structure
```js
const closure = (function() {
	
  let toggle = true;
  let count = 0;
	
  return () => {
    console.log(toggle, count);
    toggle = !toggle;
    count++;
  }
})();

closure(); // true 0
closure(); // false 1
closure(); // true 2 
```
