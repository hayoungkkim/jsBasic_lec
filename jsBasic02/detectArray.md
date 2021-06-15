배열감지
=====

전역 스코프가 하나인 일반적인 페이지에서는 instanceof 연산자를 사용하여, 배열을 구분할 수 있습니다.

```js
if(value instanceof Array) {
    // 배열일 때 실행하는 코드
}
```

페이지에 프레임이 여러 개 있다면 전역객체가 여러 개가 있고, 따라서 Array() 생성자도 각각 다르기 때문에 instanceof 연산자로 타입감지에 한계가 있습니다.

## ES5 Array.isArray()

Array.isArray() 메서드는 실행 컨텍스트와 무관하게 배열을 구분할 수 있다.

```js
Array.isArray() // ie9+


if(Array.isArray(value)) {
    // 배열일 때 실행하는 코드
}
```

```js
// Util 
function isArraySafe(value) {
    return Object.prototype.toString.call(value) === '[object Array]';
}

// Polyfill
if (!Array.isArray) {
    Array.isArray = function(value) {
        return Object.prototype.toString.call(value) === '[object Array]';
    };
}
```

[Array.isArray() - JavaScript | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/isArray)