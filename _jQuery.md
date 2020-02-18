## jQuery
  
###### install
  
###### get form data
```js
$("#id-name").serialrize();
$("#id-name").serialrizeArray();
```
  
###### ajax
```js
$.ajax({
    type: 'get',
    dataType: 'json',
    /* contentType 은 특별히 요구되는 조건이 없다면 제외시키는 것이 좋다 */
    /* contentType: 'application/json; charset=utf-8', */
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
  
###### insert [part of] html
```js
$("#id-name").load("path/path/ selector")
/* ex) $("#table").load("test/dynamicTable/ #dynamicTable") */
```
