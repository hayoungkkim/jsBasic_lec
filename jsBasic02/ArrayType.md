Array 타입 반복메서드
=====

ECMAScript 5에서 배열에 반복 메서드를 추가했습니다. 이들 메서드는 모두 매개변수를 두 개 받는데, 하나는 각 배열 데이터에서 실행할 함수이고, 옵션인 다른 하나는 함수를 실행할 스코프 객체입니다.(IE9+)

1. 각 데이터에서 실행할 함수(콜백함수)
2. 옵션 : 함수를 실행할 스코프 객체(콜백의 this값에 영향)

배열 반복메서드

* `every()` - 배열의 모든 데이터에서 콜백함수를 호출하고 반환값이 전부 true 이면 true를 반환
* `filter()` - 각 데이터에서 반환값이 true인 데이터를 새 배열에 저장하여 반환
* `forEach()` - 각 데이터에서 콜백함수를 호출, 반환값 없음
* `map()` - 각 데이터에서 콜백함수를 호출하고 그 결과를 새 배열에 저장하여 반환
* `some()` - 각 데이터에서 반환값이 하나라도 true이면 true 반환

콜백함수의 매개변수

1. 현재 값 - 배열에서 현재 처리되고 있는 값
2. 인덱스 - 현재 처리되고 있는 값의 인덱스
3. 배열 - 처리되고 있는 배열 자체

```js
var numbers = [1, 2, 3, 4, 5, 4, 3, 2, 1];

var everyResult = numbers.every(
    function(item, index, array) { return (item > 2); }
);

console.log('everyResult : ', everyResult);     // false

var someResult = numbers.some(
    function(item, index, array) { return (item > 2); }
);

console.log('someResult : ', someResult);       // true

var filterResult = numbers.filter(
    function(item, index, array) { return (item > 2); }
); 

console.log('fliterResult : ', filterResult);   // [3, 4, 5, 4, 3]
// filter() - 배열에서 특정 조건에 맞는 데이터만 쿼리할 때 유용

var mapResult = numbers.map(
    function(item, index, array) { return (item > 2); }
);

console.log('mapResult : ', mapResult);         // [false, false, true, true, true, true, true, false, false]

var mapResult2 = numbers.map(
    function(item, index, array) { return (item * 2); }
);

console.log('mapResult2 : ', mapResult2);       // [2, 4, 6, 8, 10, 8, 6, 4, 2]
// map() - 원래의 배열과 1:1로 대응하는 배열을 만들 때 유용

numbers.forEach(
    function(item, index, array) {
        console.log('array[' + index + '] = ' + item);
    }
);
// array[0] = 1
// array[1] = 2
// ...
// array[8] = 1
// forEach() - 배열에서 for문을 실행한 것과 마찬가지.
```

*****

jQuery 배열 유틸리티 메서드

* `$.each()`
    - `forEach()`
    - `every()`
    - `some()`
* `$.map()`
    - `map()`
* `$.grep()`
    - `filter()`
* `$.inArray()`
    - `indexOf()`