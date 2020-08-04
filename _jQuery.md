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
    async: false, // 이 부분을 적용해줘야 데이터를 변수에 담지 않고도 넘길 수 있다
    /* contentType 은 특별히 요구되는 조건이 없다면 제외시키는 것이 좋다 */
    /* contentType: 'application/json; charset=utf-8', */
    data: $("#searchForm").serializeArray(),
    url: "/test/findAllTestDev",
    cache: false,
    beforeSend: () => {
        //
    }
}).done(response => {
    myTest(response);
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
  
###### off() & on()
```js
$(this).off("click").on("click", function(){
    const value = $(this).children("td").children(":hidden").val();
});
```
  
###### get cell value from table on javaScript
```js
const trs = document.getElementsByTagName("tr");
		
for(let i=0; i<trs.length; i++){
  trs[i].onclick = function(){
    console.log(trs[i].getElementsByTagName("input")[0].value);
  }
}
```
###### jquery selector `:(colon)`
```js
selectOne : checkElement.is('visible')
selctAll : checkElement.is(':visible')
```
https://stackoverflow.com/questions/10552838/whats-the-purpose-of-a-leading-colon-in-a-jquery-selector
  
###### Object.prototype Issue
- When Object.prototype is used, there is a problem in jQuery  
  
[Ref.] https://stackoverflow.com/questions/33063382/jquery-error-matchexprtype-exec-is-not-a-function/33063383  
  
###### not realonly selector
```js
// input clear except readonly attribute
$('input:text:not([readonly])').addClear({
    top : -2,
    right : 6
});
```  
[Ref.] https://stackoverflow.com/questions/3708764/jquery-not-readonly-selector  
  
###### decodeRUIComponent
```js
const formData = decodeURIComponent($('#form').serialize()).replace(/,/gi,"");
console.log(formData);
```  
[Ref.] https://stackoverflow.com/questions/5632923/decoding-with-jquery-serialize    
  
###### how to get select option label
```js
$('#selecter :selected').attr('label'); 
```
[Ref.] https://stackoverflow.com/questions/2175737/how-to-get-label-of-select-option-with-jquery
