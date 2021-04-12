# util guide form
```jsx
/**
 * @description : <Select> 컴포넌트에서 가변 배열(유동적인 목록)에서 선택한 key로 value를 가져온다
 * @return {object}
 *
 * @param {array}  list       : 가변 배열
 * @param {string} compareKey : 비교값
 * @param {string} key        : 기준 key
 * @param {string} value      : 기준 value
 */
const getSelectValue = (list, compareKey, key, value) =>
    list?.find(item => item?.[key] === compareKey)?.[value];

export { getSelectValue };
```
