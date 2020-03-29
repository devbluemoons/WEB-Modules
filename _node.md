###### #text
Whitespace inside elements is considered as text,  
and text is considered as nodes. Therefore,  
in this example, the first,  
third and fifth child of the div element is a `#text` node.  
  
[Ref.]  https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Whitespace  
  
###### firstChild vs firstElementChild
- if there is whitespace between parentNode and childNode
- you will get `#text` in this case you can use `firstElementChild` instead of `firstChild`
```js
const ul = document.querySelector("ul");
console.log(ul.firstElementChild);
```
