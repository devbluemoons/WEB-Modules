## jQuery
  
###### install
  
###### get form data
```js
$("#id-name").serialrize();
$("#id-name").serialrizeArray();
$("#id-name").serialrizeObject();
```
  
###### ajax
```js
$.ajax({
    type: 'get',
    dataType: 'json',
    contentType: 'application/json; charset=utf-8',
    data: $("#searchForm").serializeArray(),
    url: "/test/findAllTestDev",
    cache: false,
    beforeSend: () => {
        //
    }
}).done(response => {
    //
}).fail(error => {
    //
}).always(response => {
    //
});
```
  
###### insert part of html
```js
$("#id-name").load("path/path/ selector")
/* $("#table").load("test/dynamicTable/ #dynamicTable") */
```
