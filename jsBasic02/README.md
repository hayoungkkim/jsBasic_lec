
Javascript Study Step02
=====

## 참조타입

* Object 타입, Array 타입, Date 타입, RegExp 타입, Function 타입 ...
* 참조 값(객체)이란 특정 **참조 타입**의 인스턴스 입니다.
* 객체(인스턴스)를 생성할 때는 new 연산자 뒤에 **생성자** 함수를 씁니다.
* 생성자는 객체(인스턴스)를 생성하는 함수입니다.

다음은 참조타입 Object와 Array의 인스턴스를 생성해서 변수에 할당합니다.

```js
var objInstance = new Object();
objInstance instanceof Object;

var arrayInstance = new Array();
arrayInstance instanceof Array;
```

### Object 타입

애플리케이션에 사용할 데이터를 저장하고 전송하는 목적에 적합합니다.

#### Object 인스턴스 생성

* new 연산자와 생성자 함수를 사용하여 인스턴스 객체 생성

```js
var obj = new Object();

obj.myProp = 'myProperty';
obj.myMethod = function() {
    console.log('This is myMethod.');
}

var obj2 = {};              // new Object() 와 동일
```

* 객체 리터럴 표기법

```js
var sherlock = {
    fullName: 'Sherlock Holmes',
    job: 'Private Detective',
    search: function() {
        console.log('나의 시선은 모든 것을 알아낸다!');
    },
    play: function() {
        console.log('바이올린 켜는 걸 좋아해');
    }
}
```

#### 프로퍼티(property), 메서드(method)

```js
var obj = {
    myProp: 'myProperty',
    myMethod: function() {
        console.log('This is myMethod.');
    }
}

// 객체의 프로퍼티 또는 메서드에 접근하는 방법
console.log( obj.myProp );
console.log( obj['myProp'] );

var variable = 'myProp';
console.log( obj[variable] );
```

> object는 property의 집합입니다.

#### Object 인스턴스 프로퍼티, 메서드

* constructor - 해당 객체를 만드는 데 쓰인 함수(생성자)를 가리킵니다. `Object()`
* hasOwnProperty(propertyName) - 프로퍼티가 프로토타입에서 상속받지 않고 해당 객체 인스턴스의 고유한 프로퍼티인지 확인합니다.
* toString() - 객체를 문자열로 변환해 반환합니다.
* valueOf() - 객체를 나타내는 문자열이나 숫자, 불리언을 반환합니다. `toString()`과 같은 값을 반환할 때가 많습니다.

```js
console.log("obj.constructor : ", obj.constructor);
console.log("obj.hasOwnProperty('myProp') : ", obj.hasOwnProperty('myProp'));
console.log("obj.hasOwnProperty('constructor') : ", obj.hasOwnProperty('constructor'));
console.log("obj.hasOwnProperty('toString') : ", obj.hasOwnProperty('toString'));
console.log("obj.toString() : ", obj.toString());
console.log("obj.valueOf() : ", obj.valueOf());
```

### Array 타입

* 데이터의 순서있는 목록입니다.
* 배열 슬롯에는 어떤 타입의 데이터라도 넣을 수 있습니다.
* 데이터를 추가하면 배열이 자동으로 커집니다.

#### Array 인스턴스 생성(배열 생성)

* new 연산자와 생성자를 사용하여 생성

```js
var arr1 = new Array();

arr1[0] = 'a';
arr1[1] = 'b';
arr1[2] = 'c';

console.log('arr1 : ', arr1);

var arr2 = new Array(1, 2, 3);              // 숫자값이 세 개 있는 배열 생성
var arr3 = new Array(3);                    // 크기가 3인 배열 생성(confuse!)

console.log('arr2 : ', arr2);
console.log('arr3 : ', arr3);

var arr4 = [];                              // new Array() 와 동일
```

* 배열 리터럴 표기법

```js
var arr1 = ['a', 'b', 'c'];

var arr2 = [
    'a',
    1,
    false,
    [1, 2, 3],
    {
        prop: 'prop',
        method: function() { /*...*/ }
    }
];
```

* 배열 접근

```js
var colors = ['red', 'blue', 'green'];

console.log(colors[0]);                 // 첫 번째 데이터 표시
colors[2] = 'black';                    // 세 번째 데이터 변경
colors[3] = 'brown';                    // 네 번째 데이터 추가
```

#### length 프로퍼티

배열에 저장된 데이터의 갯수

```js
var colors = ['red', 'blue', 'green'],
    names = [];
    
console.log(colors.length);             // 3
console.log(names.length);              // 0

// 배열의 마지막 슬롯 인덱스는 length-1
var colors = ['red', 'blue', 'green'];  // 문자열 세 개 있는 배열, length -> 3
colors[colors.length] = 'black';        // 인덱스 3에 데이터 추가
colors[colors.length] = 'brown';        // 인덱스 4에 데이터 추가
console.log(colors.length, colors);
```

#### join()

배열 데이터를 구분자와 결합하여 문자열을 반환합니다.

```js
arr.join(separator);
```

```js
var arr = ['Wind', 'Rain', 'Fire'];

console.log( arr.join() );              // 'Wind,Rain,Fire'
console.log( arr.join(', ') );          // 'Wind, Rain, Fire'
console.log( arr.join(' + ') );         // 'Wind + Rain + Fire'
console.log( arr.join('') );            // 'WindRainFire'
```

#### push() / pop()

```js
var colors = [];                                    // 배열 생성

var count = colors.push('red', 'green');            // 데이터 두개 추가
console.log('count:', count, 'colors:', colors);

count = colors.push('black');                       // 다른 데이터 추가
console.log('count:', count, 'colors:', colors);

var item = colors.pop();                            // 마지막 데이터 꺼냄
console.log('item:', item, 'colors:', colors);
```

#### shift() / upshift()

```js
var colors = [];

var count = colors.push('green', 'blue');
console.log('count:', count, 'color:', colors);

count = colors.unshift('red');                      // 첫 번째에 데이터 추가
console.log('count:', count, 'color:', colors);

var item = colors.shift();                          // 첫 번째 데이터 꺼냄
console.log('item:', item, 'colors:', colors);
```

> * 스택 LIFO : push() / pop()
> 스택 구조는 데이터의 삽입과 제거가 스택의 맨 위 한 지점에서만 발생 합니다.

> * 큐 FIFO : push() / shift()
> 큐 구조는 데이터를 마지막에 추가하고 맨 앞에서 제거 합니다.

#### concat()

기존 배열에 인자로 주어진 값이나 배열을 기존 배열과 합쳐서 **새 배열** 을 반환합니다.

```js
var newArray = originArray.concat([value1[, value2[, ...[, valueN]]]]);
```

```js
var alpha = ['a', 'b', 'c'],
    numeric = [1, 2, 3];

var newAlpha = alpha.concat(),
    alphaNumeric = alpha.concat(numeric),
    alphaNumeric2 = alpha.concat(1, [2, 3]);

console.log(newAlpha);
console.log(alphaNumeric);
console.log(alphaNumeric2);
```

#### slice()

배열에 포함된 데이터 일부를 가진 **새 배열** 을 반환합니다.

```js
newArray = originArray.slice();
newArray = originArray.slice(begin);
newArray = originArray.slice(begin, end);
```

```js
var rainbow = ['빨', '주', '노', '초', '파', '남', '보'];

var color1 = rainbow.slice(),
    color2 = rainbow.slice(2),
    color3 = rainbow.slice(1,4);

console.log(color1);
console.log(color2);
console.log(color3);
```

> concat() / slice() 메서드는 원래 배열을 변경하지 않습니다.

배열복사

```js
var arr = ['a', 'b', 'c'],
    copiedArr = arr;
    
arr.pop();
console.log('arr:', arr, 'copiedArr:', copiedArr);
```

```js
var arr = ['a', 'b', 'c'],
    copiedArr = arr.slice(),
    copiedArr2 = arr.concat();
    
arr.pop();
console.log('arr:', arr, 'copiedArr:', copiedArr, 'copiedArr2:', copiedArr2);
```

#### splice()

배열에 요소를 추가하거나 삭제하여 배열을 변경하고, 삭제된 배열을 반환합니다.

```js
array.splice(start)
array.splice(start, deleteCount)
array.splice(start, deleteCount, item1, item2, ...)
```

```js
var colors = ['red', 'green', 'blue'];
    removed = colors.splice(1);
    
console.log('removed:', removed, 'colors:', colors);
```

```js
var colors = ['red', 'green', 'blue'];
    removed = colors.splice(0, 1);
    
console.log('removed:', removed, 'colors:', colors);
```

```js
var colors = ['red', 'green', 'blue'];
    removed = colors.splice(1, 1, 'black', 'gold');
    
console.log('removed:', removed, 'colors:', colors);
```

#### sort() / reverse()

배열의 순서를 조작합니다.

* sort() - 배열의 데이터를 문자열로 변환하여 오름순으로 정렬합니다.
* reverse() - 배열의 데이터를 역순으로 변경합니다.

```js
var values = [1, 2, 3, 4, 5];
values.reverse();

console.log(values);                // 5,4,3,2,1
```

> 배열 자체를 변경합니다.(파괴적 메서드)

> sort() 메서드는 기본적으로 데이터를 오름차순을 정렬합니다.
> sort() 메서드는 이를 위해 이면에서 String() 함수를 함수를 호출해 데이터를 문자열로 변환한 후 이를 비교하여 순서를 판단합니다.
> 이는 숫자로 이루어진 배열에도 똑같이 동작하여 상식적이지 않은 결과를 나타냅니다.

```js
var values = ['a', 'A', 'C', 'c', 'b', 'B'];
values.sort();

console.log(values);                // A,B,C,a,b,c
```

```js
var values = [0, 1, 5, 10, 15];
values.sort();

console.log(values);                // 0,1,10,15,5
```

비교함수로 정렬규칙을 정할 수 있습니다.

```js
arr.sort(compareFunction);
```

> 비교함수의 역할 - 음수나 0, 양수 중 하나를 반환합니다.
> * 첫 번째 매개변수가 두 번째 매개변수보다 앞에 있어야 한다면 음수 반환
> * 첫 번째 매개변수가 두 번째 매개변수보다 뒤에 있어야 한다면 양수 반환
> * 두 매개변수의 순서가 같다면 0

```js
function compare(value1, value2) {
    if(value1 < value2) {
        return -1;
    } else if(value1 > value2) {
        return 1;
    } else {
        return 0;
    }
}

var values = [0, 1, 5, 10, 15];
values.sort(compare);

console.log(values);            // 0,1,5,10,15
```

```js
// 데이터들이 숫자로만 되어있다면 단순히 빼면됩니다.
function compare(value1, value2) {
    return value1 - value2;
}
```

> jsBasic_prac02/array.html
> - data 배열에 있는 객체를 직급레벨 순서에 맞게 정렬해보세요.

[Array.prototype.sort() - JavaScript | MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)

### Date 타입

날짜와 시간 정보를 가지고 있는 객체, 날짜와 시간을 저장할 때 1970년 1월 1일 자정부터 몇 밀리초가 지났는지 나타내는 숫자를 사용합니다.

```js
var now = new Date();

console.log('now : ', now);
console.log('now.getTime() : ', now.getTime());
console.log('now.valueOf() : ', now.valueOf());
console.log('+now : ', +now);
console.log('now.getFullYear() : ', now.getFullYear());
```

```js
// 년, 월 인덱스(0~11), 일(1~31), 시(0~23), 분, 초, 밀리초
// 년, 월은 필수 매개변수

// 2000년 1월 1일 0시
var y2k = new Date(2000, 0);

// 2005년 5월 5일 오후 5시 55분 55초
var allFives = new Date(2005, 4, 5, 17, 55, 55);
```

#### 날짜/시간 메서드

|      | 가져오기          | 설정하기          | 특징          |
| ---- | ------------- | ------------- | ----------- |
| 년    | getFullYear() | setFullYear() | 4자리 숫자 연도   |
| 월    | getMonth()    | setMonth()    | 월 인덱스(0~11) |
| 일    | getDate()     | setDate()     | 일(1~31)     |
| 요일   | getDay()      | setDay()      | 요일 인덱스(0~6) |
| 시간   | getHours()    | setHours()    | 0~23        |
| 분    | getMinutes()  | setMinutes()  | 0~59        |
| 초    | getSeconds()  | setSeconds()  | 0~59        |

> jsBasic_prac02/date.html
> * 오늘 날짜를 년/월/일 형태로 출력하기
> * 현재시간을 시:분:초 형태로 출려하기
> * 1월 1일이면 'Happy new year!' 를 출력하기, 그 외에는 오늘 날짜 출력하기

#### Date.now()

ECMAScript 5에서 Date 객체에 추가된 정적 메서드, 현재 시각을 밀리초 표현으로 반환합니다.(IE9+)

```js
// 시작시간
var start = Date.now();

// 실행 시간을 측정할 함수
doSomething();

// 끝난 시간, 실행 시간
var stop = Date.now(),
    result = stop - start;
```

```js
// 시작시간
var start = +new Date();

// 실행 시간을 측정할 함수
doSomething();

// 끝난 시간, 실행 시간
var stop = +new Date(),
    result = stop - start;
```

### RegExp 타입

ECMAScript는 RegExp 타입을 통해 정규표현식을 지원합니다.

```js
var expression = /pattern/flags;
```

```js
var pattern1 = new RegExp('[bc]at', 'i');

var pattern2 = /[bc]at/i;
```

**flag**

* g : 문자열 전체에 매치할 때
* i : 대/소문자를 구분하지 않을 때
* m : 여러 줄 모드일 때

```js
// 'bat' 나 'cat' 중 처음 나온 것에 일치, 대소문자 구분 없음
var pattern1 = /[bc]at/i;

// 처음 나온 '[bc]at' 에 일치, 대소문자 구분 없음
var pattern2 = /\[bc\]at/i;

// 'at' 로 끝나는 세 글자 모두 일치, 대소문자 구분 없음
var pattern3 = /.at/gi;

// '.at' 에 모두 일치, 대소분자 구분 없음
var pattern4 = /\.at/gi;
```

[RegExpType detail](RegExpType.md)

[정규식 - JavaScript | MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Guide/%EC%A0%95%EA%B7%9C%EC%8B%9D)

[RegExr: Learn, Build, & Test RegEx](http://www.regexr.com/39etf)

### 함수

자바스크립트에서 함수는 객체입니다. 모든 함수는 Function 타입의 인스턴스이며 다른 참조타입과 마찬가지로 프로퍼티와 메서드가 있습니다.

* 함수는 실행문장들을 집합처럼 감싸고 있습니다.
* 함수는 코드의 재사용이나 정보의 구성 및 은닉 등에 사용하고, 객체의 행위를 지정하는 데 사용합니다.
* 함수는 보통 함수선언 문법으로 정의하거나 함수 표현식으로 변수에 할당합니다.
* 함수와 다른 참조타입과 구분되는 특징은 호출할 수 있다는 것입니다.

```js
// 함수 선언
function functionName(param0, param1, ..., paramN) {
    statements;
}

// 함수 호출/실행
functionName(arg1, arg2, ..., argN);

function sayHi(name, message) {     // 함수 선언
    console.log('Hello ' + name + ', ' + message);
}

sayHi('Bob', 'How are you?');       // 함수 호출
```

```js
// 함수표현식 - 익명함수를 변수에 할당
var sum = function(num1, num2) {
    return num1 + num2;
};
```

* Parameter(인자, 매개변수) : 함수 선언과 함수 내부에서 사용하는 변수
* Argument(인수) : 함수 호출시 입력 값
* 함수호출 시 매개변수는 인수로 초기화 됩니다. 인수가 전달되지 않은 매개변수는 `undefined`로 초기화 됩니다.

```js
function helloEveryone(name0, name1, name2) {
    console.log('Hello ' + name0 + ', ' + name1 + ', ' + name2);
}

helloEveryone('cat', 'dog');
```

#### 반환 값(return)

* 함수를 호출하면 함수 몸체의 첫 문장부터 끝까지 실행하고 프로그램의 제어가 함수를 호출한 부분으로 반환됩니다.
* 함수는 꼭 값을 반환하지 않아도 되지만, 언제든 `return` 문 뒤에 반환할 값을 써서 값을 반환하고 함수를 종료할 수 있습니다.

```js
function sum(num1, num2) {
    return num1 + num2;
}

// 함수를 호출하여 실행된 값을 전달받아 사용할 수 있다.
var result = sum(5, 10);
console.log(result);
```

* 함수는 return 문을 만나는 즉시 실행을 멈추고 빠져나옵니다. 따라서 return 문 뒤의 코드는 실행되지 않습니다.

```js
function sum(num1, num2) {
    return num1 + num2;
    console.log('Added!!');         // 실행되지 않습니다.
}

function diff(num1, num2) {
    if(num1 < num2) {
        return num2 - num1;
    } else {
        return num1 - num2;
    }
}
```

> return 문 뒤에 반환 값을 쓰지 않아도 됩니다. 이렇게 하면 함수는 return 문을 만나는 즉시 실행을 멈추고 `undefined` 를 반환합니다.

#### 값처럼 쓰는 함수

함수도 값이 올 수 있는 곳이라면 어디든 사용할 수 있습니다. 함수를 변수에 저장하거나, 함수의 매개변수 값으로 넘기거나, 함수의 실행결과로 함수를 반환하는 것이 가능합니다.

```js
// 함수를 변수에 저장하거나,
var callFunction = function(func, param) {
    return func(param);
}

function add10(num) {
    return num + 10;
}

// 함수의 인자값으로 넘길 수 있습니다.
var result1 = callFunction(add10, 10);
console.log(result1);                       // 20

function getGreeting(name) {
    return 'Hello, ' + name;
}

var result2 = callFunction(getGreeting, 'Bob');
console.log(result2);                       // `Hello, Bob';
```

```js
// 함수의 실행결과로 함수를 반환할 수 있습니다.
function makeCounter() {
    var count = 0;

    return function() {
        count++;
        console.log(count);
    }
}

var countSomething = makeCounter();
countSomething();
countSomething();
```

#### 함수선언 호이스팅

자바스크립트 엔진이 코드를 평가할 때 함수 선언을 먼저 찾은 다음 함수 선언을 끌어올립니다.(hoist)

```js
// 함수선언
console.log( sum(10, 10) );

function sum(num1, num2) {
    return num1 + num2;
}
```

```js
// 함수표현식
console.log( sum(10, 10) );

var sum = function(num1, num2) {
    return num1 + num2;
}
```

```js
// 함수선언
function sum(num1, num2) {
    console.log( num1 + ' + ' + num2);
}

sum(10, 20);

function sum(num1, num2) {
    console.log(num1 +num2);
}

sum(30, 40);
```

```js
// 함수표현식
var sum = function(num1, num2) {
    console.log(num1 + ' + ' + num2);
}

sum(10, 20);

var sum = function(num1, num2) {
    console.log(num1 + num2);
}

sum(30, 40);
```

#### 변수 호이스팅

```js
var scope = 'global';

function show() {
    console.log(scope);
}
```

```js
var scope = 'global';

function show() {
    console.log(scope);
    var scope = 'local';
    console.log(scope);
}
```

함수안에서 지역변수가 선언되기 전에 변수 scope를 참조한 경우 `undefined`가 반환됩니다. 
지역변수 scope 자체는 함수 전체에서 유효하지만, 값은 아직 대입되지 않았기 때문입니다. 

지역변수가 대입되어 있지 않았지만 전역변수를 참조하는 않는 것은 변수가 함수내부에서 호이스팅 되었기 때문입니다. 이런 것은 직감적으로 이해하기 어려운 결과이므로 의도적으로 사용하지 않는 것이 좋습니다.

#### 함수 프로퍼티와 메서드

* length

```js
function sayName(name) {
    console.log(name);
}
function sum(num1, num2) {
    return num1 + num2;
}
function sayHi() {
    console.log('Hi');
}

console.log(sayName.length);
console.log(sum.length);
console.log(sayHi.length);
```

* prototype - 참조 타입의 인스턴스 메서드가 존재하는 객체입니다.

* apply() / call() - 함수를 호출하면서 컨텍스트와 인수를 넘길 수 있습니다..

```js
function sum(num1, num2) {
    return num1 + num2;
}

function callSum1(num1, num2) {
    return sum.apply(this, [num1, num2]);   // 배열로 인수를 넘깁니다.
}
function callSum2(num1, num2) {
    return sum.apply(this, arguments);     // arguments 객체를 넘깁니다.
}

console.log(callSum1(10, 10));              // 20
console.log(callSum2(10, 10));              // 20

function callSum3(num1, num2) {
    return sum.call(this, num1, num2);
}
```

```js
// apply()와 call() 을 사용해서 this 를 변경할 수 있습니다..

window.color = 'red';
var o = { color: 'blue' };

function sayColor() {
    console.log(this.color);
}

sayColor()                  // red

sayColor.call(this);        // red
sayColor.call(window);      // red
sayColor.call(o);           // blue
```

> jsBasic_prac02/function.html
> * 함수 연습문제

### 원시 래퍼 타입

Boolean(), Number(), String() 은 원시 값을 편리하게 조작하기 위해 디자인된 참조 타입입니다.

```js
var s1 = 'string',
    s2 = s1.substring(2);
    
var s1 = 'string',
    s2 = new String(s1).substring(2);
```