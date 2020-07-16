###### how to get the last character of a string
```js
const test = "abcdefg";
console.log(test.slice(-1));
```
[Ref.] https://stackoverflow.com/questions/3884632/how-to-get-the-last-character-of-a-string  
###### how to cast number to string
```js
let sample = 1234567890;
console.log(typeof sample);

sample = sample.toString();
console.log(typeof sample);
```
###### number Formatter
```js
let sample = 1234567890;
console.log(new Intl.NumberFormat().format(sample));
```

###### convert boolean to string
```js
let toggle = true;
console.log(typeof toggle);

toggle = Boolean(toggle).toString();
console.log(typeof toggle);
```
