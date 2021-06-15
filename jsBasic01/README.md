
# Javascript Study Step01

## 자바스크립트 학습(기술 관점)

* 코어(ECMA Script)
    - 프로그래밍 언어로서 문법, 타입, 선언문, 예약어, 연산자, 객체
    - ECMAScript 3.1
    - ECMAScript 5 (2009)
    - ECMAScript 6 (ES6 : 2015)
    - ECMAScript 2016 (ES7 : 2016)

* 브라우저 객체 모델(BOM)
    - 브라우저와 상호작용하는 메서드와 인터페이스를 제공

* 문서 객체 모델(DOM)
    - 웹 페이지 콘텐츠를 조작하는 메서드와 인터페이스를 제공

* 이벤트(브라우저 호환성 문제에 유의)
    - 사용자의 액션을 알아내고, 이에 반응하는 함수 정의

* 데이터 가져오기
    - 페이지 갱신 없이 서버로부터 데이터 가져오기

*****

## 언어의 기초

### 대소문자 구문

변수, 함수이름, 연산자 모두 대소문자 구분

```js
var test = "Hello world";
console.log(Test);
```

### 문장 끝에 세미콜론

```js
var test = "Hello world";
console.log(test);
```

### 한 줄 주석

```js
// 한 줄 주석입니다.
```

### 여러 줄 주석

```js
/*
    이런 형식을 서서
    주석을 여러 줄로 쓸 수 있습니다.
*/
```

### 자바스크립트 위치

```html
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <title>Sample</title>
    <link rel="stylesheet" type="text/css" href="../css/common.css">
    <link rel="stylesheet" type="text/css" href="../css/content.css">
    <!-- 공용 스크립트 선언 -->
    <!-- 전통적으로 script 요소는 head 요소 안에 쓰는 것이 일반적이 였으나 -->
</head>
<body>
    <div id="wrap">
        <div id="content">
            
        </div>
    </div>
    <!-- 공용 스크립트 선언 -->
    <script type="text/javascript" src="../js/libs/jquery.min.js"></script>
    <script type="text/javascript" src="../js/libs/jquery.easing.min.js"></script>
      <script type="text/javascript" src="../js/common.js"></script>
    <!-- 해당페이지 전용 스크립트 선언 -->
    <script type="text/javascript" src="../js/page/test.js"></script>
    <script type="text/javascript">
        (function() {
            
        })();
    </script>
</body>
</html>
```

### 식별자(Identifier)

식별자란 변수나 함수, 프로퍼티, 함수 매개변수의 이름

* 첫 번째 문자는 반드시 글자나 밑줄( _ ), 달러($) 중 하나(숫자 사용불가)
* 예약어(키워드) 사용불가

- 키워드 : 스크립트에서 수행되어야 할 동작을 식별하는 단어(제어문의 시작과 끝 / 특정한 조작 목적)
- 예약어 : 자바스크립트에서 사용하고 있는 혹은, 사용될 예정인 이름

```js
abstract boolean break byte case catch char class const continue debugger default delete do double else enum export extends false final finally float for function goto if implements import in instanceof int interface long native new null package private protected public return short static super switch synchronized this throw throws transient try typeof var volatile void while with...
```

관습적으로 카멜케이스 표기법을 사용

```js
firstSecond
myCar
```

*****

## 변수

* 데이터의 저장소 역할
* 단순한 데이트 원시 값과 여러 값으로 구성되는 객체를 가리키는 참조 값 
* 자바스크립트는 느슨한 타입

```js
var message; // var 키워드, message 식별자

var message = "Hi";     // 할당
var message = 20;       // 어떤 값이든
var message = true;     // 할당할 수 있다.
```

### 변수 범위

* 모든 변수에는 유효범위(스코프)가 있습니다. 변수에 접근할 수 있는 범위이며 그 영역 바깥에서는 변수에 접근 할 수 없습니다.
* 변수에는 전역 변수(global variable)와 지역 변수(local variable)이 있으며,
* 전역 변수는 자바스크립트 코드 전체에서 사용할 수 있고,
* 지역 변수는 선언된 함수 내부에서만 사용할 수 있습니다.

```js
var scope = 'Global';

function show() {
    return scope;
}

console.log(show());
console.log(scope);
```

```js
function show() {
    var scope = 'Local';
    return scope;
}

console.log(show());
console.log(scope);
```

```js
var scope = 'Global';

function show() {
    var scope = 'Local';
    return scope;
}

console.log(show());
console.log(scope);
```

* 함수 안에서 var 연산자는 변수를 로컬 스코프(함수 스코프)에 정의한다.
* 함수 안에서 var 키워드를 써서 변수를 정의하면 해당 변수는 함수를 종료하는 즉시 파괴된다.

> var 없이 변수를 선언하고 값을 주면 어떻게 될까?

```js
function show(){
    scope = "Do Not this";
    return scope;
}

console.log(show());
console.log(scope);
```

```js
function show() {
  var withVar = noVar = 'confuse';
}

show();
console.log(noVar);
console.log(withVar);
```

> anti-pattern

*****

## 데이터 타입

* undefined
* null
* 숫자
* 문자
* 불리언
* 객체 Object : 숫자, 문자, 불리언 값이 아닌 타입들(Object, Array, Date, RegExp, Function...)

### typeof 연산자

```js
var message = "some string";
console.log(typeof message);    // "string"
console.log(typeof 95);         // "number"
```

* 정의되지 않은 변수 : "undefined"
* 불리언 : "boolean"
* 문자열 : "string"
* 숫자 : "number"
* 함수를 제외한 객체 또는 null : "object"
* 함수 : "function"

### 원시 값과 참조 값

값을 변수에 저장하는 방법의 차이

* 원시 값(Primitive value) - 단순한 데이터, 실제 값 자체
* 참조 값(Reference value) - 값을 실제로 저장하는 메모리 상의 주소

```js
var num1 = 5,
    num2 = num1,
    anotherNum = 5;

console.log(num1 === num2);
console.log(num1 === anotherNum);
```

```js
var arr1 = [1, 2, 3],
    arr2 = arr1,
    anotherArr = [1, 2, 3];
    
console.log(arr1 === arr2);
console.log(arr1 === anotherArr);
arr1.push('a');
console.log(arr1);
console.log(arr2);
console.log(anotherArr);
```

```js
var arr1 = [1, 2, 3],
    arr2 = arr1,
    anotherArr = arr1.slice();
    
console.log(arr1 === arr2);
console.log(arr1 === anotherArr);
arr1.push('a');
console.log(arr1);
console.log(arr2);
console.log(anotherArr);
```

### undefined

```js
var message;                        // 이 변수는 선언되었지만 값을 초기화 하지 않았습니다.
console.log(message);               // undefined
console.log(message === undefined); // true
```

```js
var message;
// var age                          // 이 변수는 선언되지 않았습니다.

console.log(message);               // undefined
console.log(age);                   // ReferenceError
```

1. 변수를 선언하고 그 변수에 값을 대입하지 않은 경우
2. 객체의 정의되지 않은 프로퍼티에 접근하는 경우
3. 함수 매개변수를 정의했으나 그 매개변수에 값이 전달되지 않은 경우

### null

빈 객체를 가리키는 포인터

### 불리언 타입

| 데이터타입 | true로 변환되는 값              | false로 변환되는 값 |
| ---------- | ------------------------------- | ------------------- |
| 불리언     | true                            | false               |
| 문자열     | 비어있지 않은 문자열 모두       | " " (빈문자열)      |
| 숫자       | 0이 아닌 모든 숫자, 무한대 포함 | 0, NaN              |
| 객체       | 모든 객체                       | null                |
| undefined  | 해당 없음                       | undefined           |

> if 문 같은 제어문은 데이터 타입을 자동으로 불리언으로 변환하기 때문에, 변환규칙을 이해하고 있어야 한다.

```js
var message = "Hello world!";
if (message) {
    console.log("Value is true");
}
```

### 숫자타입

```js
var intNum = 23;
var intNum1 = 2;
var floatNum = 0.05;
var floatNum1 = 0.01;
var numMax = Number.MAX_VALUE;

var sum = intNum + floatNum;
var sum1 = intNum + floatNum * intNum1;
var sum2 = (intNum + floatNum) * intNum1;
var sum3 = floatNum + floatNum1;

console.log('sum : ', sum, typeof sum);
console.log('sum1 : ', sum1, typeof sum1);
console.log('sum2 : ', sum2, typeof sum2);
console.log('sum3 : ', sum3, typeof sum3);
console.log('numMax : ', numMax, typeof numMax);
```

**소수점 연산 오류**

```js
var a = 0.1;
var b = 0.2;

if (a + b === 0.3) {
    console.log('You got 0.3');
} else {
    console.log('Something Wrong');
}
console.log(a + b);
```

### 숫자 변환

```js
var str = "3.14";
console.log(str, typeof str);

var num = parseInt(str);
var num1 = parseFloat(str);
var num2 = Number(str);
var num3 = +str;
console.log(num, typeof num);
console.log(num1, typeof num1);
console.log(num2, typeof num2);
console.log(num3, typeof num3);

var str1 = "3.14 PIE";
console.log(parseInt(str1), parseFloat(str1));

console.log(parseInt("I like 7"));
console.log(Number('Hello World!'));
console.log(Number(''));
console.log(Number('000011'));
console.log(Number(true));
console.log(Number(null));
```

> 숫자형 값 중에는 NaN(Not a Number) 라는 특별한 값이 있습니다. 이 값은 숫자를 반환할 것으로 의도한 조작이 실패했을 때 반환하는 값입니다.

### 진수 표기

* 10진수 : 숫자만 쓴다
* 8진수 : 숫자 앞에 0을 붙인다
* 16진수 : 숫자 앞에 숫자 0 과 소문자 x를 붙인다

```js
var num = 12;
var numOct = 012;
var numHex = 0x12;
console.log(num);
console.log(numOct);
console.log(numHex);

var phoneNumber1 = 01012341234;
var phoneNumber2 = 01012345678;
var phoneNumber3 = `01012341234`;
console.log(phoneNumber1);
console.log(phoneNumber2);
console.log(phoneNumber3);

var numOct2 = 079;
console.log(numOct2);               // 9가 범위를 벗어 났으며 79로 간주

var pNum1 = parseInt('10', 2);      // 2진수 10은 10진수 2
var pNum2 = parseInt('10', 8);      // 8진수 10은 10진수 8
var pNum3 = parseInt('10', 10);     // 10
var pNum4 = parseInt('10', 16);     // 16진수 10은 10진수 16
```

> `partseInt()`에  진법 매개변수를 넘기지 않으면 브라우저에서 숫자의 형식을 판단하도록 일임하는 것이므로 의도와 다른 결과가 나올 수 있습니다. 항상 진법 매개변수를 명시해서 오류를 예방하는 편이 좋습니다.

### Math 객체

수학연산에 관련된 객체

```js
var num = 3.1;
var num1 = 3.6;

// 반올림, 버림, 올림
console.log(Math.round(num));
console.log(Math.round(num1));
console.log(Math.floor(num1));
console.log(Math.ceil(num));

// 0(포함) ~ 1(미포함) 사이의 난수 값
var randomNum = Math.random();
console.log(randomNum);

// min(포함)과 max(포함) 사이의 임의의 정수 값
// Math.round()를 사용하면 고르지 않은 분포를 얻게된다!
// Math.floor( Math.random() * (max - min + 1) ) + min;

// 1과 100 사이의 난수
var num2 = Math.floor( Math.random() * 100 ) + 1;

// 2와 10 사이의 난수
var num3 = Math.floor( Math.random() * 9 ) + 2;
```

[Math - JavaScript | MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Math)

### 문자열 타입

큰 따옴표나(`" "`) 작은따옴표(`' '`)로 감싸서 표현

```js
var myString = "Javascript '기초' 과정";
```

**유용한 문자 리터럴**

| 리터럴                | 의미                      |
| --------------------- | ------------------------- |
| `\n`                  | 줄바꿈                    |
| `\t`                  | 탭                        |
| `\b`                  | 백스페이스                |
| `\"`                  | " 표시(이스케이프 시퀀스) |
| `\'`                  | ' 표시(이스케이프 시퀀스) |
| `\uNNNNN`(N은 16진수) | 16진수로 된 유니코드 문자 |

```js
var str = 'It\'s alright';
```

### 문자열 생성

**문자열 객체의 인스턴스 생성**

```js
// String 객체타입의 인스턴스는 String 객체타입의 프로퍼티 또는 메서드 사용 가능
var strObj = new String('Javascript');
console.log('strObj.length: ', strObj.length);

var newStrObj = strObj.toUpperCase();
console.log('newStrObj: ', newStrObj);
```

**리터럴 방식으로 생성**

```js
// 리터럴 방식으로 생성하여도 String 객체타입의 인스턴스 처럼 프로퍼티와 메서드 사용 가능
var strLiteral = "Javascript";
console.log('strLiteral.length: ', strLiteral.length);

var newStrLiteral = strLiteral.toUpperCase();
console.log('newStrLiteral: ', newStrLiteral);
```

리터럴 방식으로 생성한 문자열과 String 생성자로 생성한 문자열의 차이점

```js
var strObj = new String('Javascript');
var strLiteral = "Javascript";

console.log('typeof strObj: ', typeof strObj);          // object
console.log('typeof strLiteral: ', typeof strLiteral);  // string
```

> Javascript 에서는 주로 리터럴 방식으로 문자열을 선언합니다.

### 문자열 연결

* `+` 연산자를 사용하여 문자열을 연결합니다.
* 문자열은 일단 만들어지면 그 값을 바꿀 수 없고, 변수에 저장된 문자열을 바꾸려하면 기존의 문자열을 파괴하고 새 문자열로 변경됩니다.

```js
var lang = "Java";
lang = lang + "Script";

console.log(lang);
```

### 문자열 프로퍼티

* length

```js
var str = "Hello world!";

console.log(str.length);
```

### 문자열 메서드

* charAt(index) : 인덱스에 해당하는 문자열 찾기

```js
var str = "Hello world!";

console.log(str.charAt(0), str.charAt(6));
```

**문자열 검색**

검색하려는 문자열이 존재하지 않을 경우 -1을 반환

* indexOf(searchValue)
* indexOf(searchValue, start)
* lastIndexOf(searchValue)
* lastIndexOf(searchValue, start)

```js
var str = "I'am Sam!";

console.log(str.indexOf('am'));
console.log(str.indexOf('am', 5));
console.log(str.lastIndexOf('am'));
console.log(str.lastIndexOf('am', 5));
```

| I   | '   | a   | m   |     | S   | a   | m   | !   |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0   | 1   | 2   | 3   | 4   | 5   | 6   | 7   | 8   |

**문자열 추출**

* substring(start, end)
* substr(start, length)

```js
var str = "I'am Sam!";

console.log(str.substring(2));
console.log(str.substr(2));
console.log(str.substring(2, 6));
console.log(str.substr(2, 6));
```

| I   | '   | a   | m   |     | S   | a   | m   | !   |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0   | 1   | 2   | 3   | 4   | 5   | 6   | 7   | 8   |

**문자열 분할**

* split(separator, limit)

```js
var str = 'apple, banana, pineapple, magosteen!';
var strArr = str.split(',');
var strArr1 = str.split(',', 1);

console.log(strArr);
console.log(strArr1);
console.log(str);
```

**대소문자 변경**

* toUpperCase()
* toLowerCase()

```js
var str = 'I like Sam.';

console.log(str.toUpperCase());
console.log(str.toLowerCase());
```

[String#Method - JavaScript | MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/String#Methods)

### 객체타입

ECMAScript 에서 객체는 데이터와 기능의 집합입니다.

* Object 타입
* Array 타입
* Date 타입
* RegExp 타입
* Function 타입
* 원시래퍼타입(Boolean타입, Number타입, String타입)
* Global객체
* Math객체

```js
// 생성자 생성방식
var objInstance = new Object();
objInstance.property = 'value';
objInstance.method = fucntion() { 
    console.log('메서드 입니다');
 }

// 객체리터럴 표기법
var objInstance = {
    property: 'value',
    method: function() { 
        console.log('메서드 입니다');
     }
}
```

## 연산자

### 산술 연산자

| 연산자 | 읽기         | 기능        | 사용법    | 결과 |
| ------ | ------------ | ----------- | --------- | ---- |
| +      | 플러스       | 덧셈        | a = 5 + 5 | 10   |
| -      | 마이너스     | 뺄셈        | a = 5 - 5 | 0    |
| *      | 애스터리스트 | 곱셈        | a = 5 * 5 | 25   |
| /      | 슬래시       | 나눗셈      | a = 5 / 5 | 1    |
| %      | 모듈로       | 나머지 연산 | a = 5 % 5 | 0    |

```js
var odd = 9;
console.log(odd % 2 === 1);
```

**덧셈 연산자의 피연산자 중 문자열이 있을 때**

* 피연산자 모두 문자열 이라면 첫 번째 문자열 뒤에 두 번째 문자열을 합칩니다.
* 피연산자 중 하나가 문자열이면, 다른 피연산자를 문자열로 변환하고 두 문자열을 합칩니다.

```js
var result1 = 5 + 5;        // 숫자 두 개
console.log(result1);       // 10

var result2 = 5 + '5';      // 숫자 한 개와 문자열 한개
console.log(result2);       // '55'

var num1 = 5,
    num2 = 10;
    
var message = 'The sum of 5 and 10 is ' + num1 + num2;
console.log(message);
```

### 대입 연산자(할당)

```js
var a = a + 2;      // 1. a + 2 연산
                    // 2. a = (a + 2) 대입
                    
var a += 2;
```

**복합 대입 연산자**

| 연산자 | 기능          | 사용법         | 결과 |
| ------ | ------------- | -------------- | ---- |
| +=     | 더해서 대입   | a = 5; a += 5; | 10   |
| -=     | 빼서 대입     | a = 5; a -= 5; | 0    |
| *=     | 곱해서 대입   | a = 5; a *= 5; | 25   |
| /=     | 나눠서 대입   | a = 5; a /= 5; | 1    |
| %=     | 나머지를 대입 | a = 5; a %= 5; | 0    |

### 증가 / 감소 연산자

| 연산자 | 명칭        | 기능               |
| ------ | ----------- | ------------------ |
| ++     | 증가 연산자 | 변수의 값을 1증가  |
| --     | 감소 연산자 | 변수의 값을 1 감소 |

```js
var a = 1,
    b = ++a;
console.log(a, b);

var a = 1;
a = a + 1;
var b = a;
console.log(a, b);
```

```js
var a = 1,
    c = a++;
console.log(a, c);

var a = 1;
var c = a;
a = a + 1;
console.log(a, b);
```

### 비교 연산자

조건을 만족하면 참(true), 만족하지 않으면 거짓(false) 반환

| 연산자 | 기능      | 사용법  | 의미                                               |
| ------ | --------- | ------- | -------------------------------------------------- |
| ==     | 같다      | a == b  | a와 b의 값은 같다.                                 |
| ===    | 같다      | a === b | a와 b의 값과 데이터 타입이 같다.                   |
| <      | 작다      | a < b   | a는 b보다 작다.                                    |
| >      | 크다      | a > b   | a는 b보다 크다.                                    |
| <=     | 이하      | a <=    | a는 b보다 작거나 같다.                             |
| >=     | 이상      | a >=    | a는 b보다 크거나 같다.                             |
| !=     | 같지 않다 | a != b  | a와 b는 같지 않다.                                 |
| !==   | 같지 않다 | a !== b | a와 b는 값이 같지 않거나, 데이터 타입이 같지 않다. |

```js
console.log(1 == '1');
console.log(1 === '1');
```

>anti-pattern

### 3항 연산자

```js
variable = boolean_expression ? true_value : false_value;

var max = (num1 > num2) ? num1 : num2;
```

```js
// 위의 3항식을 풀어쓰면 아래와 같다.
var num1 = 4,
    num2 = 10,
    max = 0;
    
if(num1 > num2) {
  max = num1;
} else {
  max = num2;
}
```

### 논리 연산자

여러 개의 조건식을 조합할 때 사용

| 연산자 | 기능       | 사용법                     | 의미                            |
| ------ | ---------- | -------------------------- | ------------------------------- |
| &&     | 그리고     | (a >= 10) && (a < 50)      | a는 10 이상이고, 50 미만입니다. |
| `ㅣㅣ` | 또는       | (a == 1) `ㅣㅣ` (a == 100) | a는 1 또는 100 입니다.          |
| !      | ~이 아니다 | !(a == 100)                | a는 100이 아닙니다.             |

**`&&` 논리 AND**

| 피연산자1 | 피연산자2 | 결과  |
| --------- | --------- | ----- |
| true      | true      | true  |
| true      | false     | false |
| false     | true      | false |
| false     | false     | false |

첫 번째 피연산자가 false 이면 두 번째 피연산자는 평가하지 않는다.

```js
var found = false;
var result = found && undeclaredVariable;	// 에러 없음
console.log(result);
```

**`||` 논리 OR**

| 피연산자1 | 피연산자2 | 결과  |
| --------- | --------- | ----- |
| true      | true      | true  |
| true      | false     | true  |
| false     | true      | true  |
| false     | false     | false |

첫 번째 피연산자가 true 이면 두 번째 피연산자는 평가하지 않는다.

```js
var found = true;
var result = found || undeclaredVariable;	// 에러 없음
console.log(result);
```

**`!` 논리 NOT**

* 피연산자가 `객체`이면 `false`를 반환합니다.
* 피연산자가 `빈 문자열`이면 `true`를 반환합니다.
* 피연산자가 `비어 있지 않은 문자열`이면 `false`를 반환합니다.
* 피연산자가 `숫자 0`이면 `true`를 반환합니다.
* 피연산자가 `0이 아닌 숫자`이면 `false`를 반환합니다.
* 피연산자가 `null` 이면 `true`를 반환합니다.
* 피연산자가 `undefined` 이면 `true`를 반환합니다.

```js
console.log(!false);
console.log(!'javascript');
console.log(!0);
console.log(!'');
console.log(!12345);

console.log(!!false);
console.log(!!'javascript');
console.log(!!0);
console.log(!!'');
console.log(!!12345);

// Boolean() 함수를 호출 것과 같음
```

*****

## 제어문장

### if문 

조건에 따라 분기처리하기

```js
if(condition1) {
    // condition1이 true일 경우 실행
} else if(condition2) {
    // condition2가 true일 경우 실행
} 
// ...
else {
    // 어느 조건식도 true가 아닌 경우에 실행
}

/*
    num의 값이 짝수일 경우, '~는 짝수입니다.' 를 출력,
    짝수가 아닐 경우에는 '~는 홀수입니다.' 를 출력하기
*/

var num = 4;

if(num % 2 == 0) {
    console.log(num + '은 짝수입니다.');
} else {
    console.log(num + '은 홀수입니다.');
}

// 삼항연산자로 표현하기
var num = 4,
    str = '';
    
str = (num % 2 == 0) ? num + '은 짝수입니다.' : num + '는 홀수입니다.';
console.log(str);
```

> condition(조건)에는 어떤 표현식이든 쓸 수 있으며, ECMAScript는 해당 표현식의 결과에 Boolean() 함수를 호출해 불리언 값으로 바꿉니다.

```js
if(i > 25)
    console.log('Greater than 25.');            // 한 줄 문장
else {
    console.log('Less than or equal to 25.');   // 블록문장
}
```

**단 한 줄의 코드만 실행하더라고 코드 블록을 쓰기를 권합니다. 조건에 따라 어느 문장을 실행하는지 분명하게 파악 가능합니다.**

### switch문

변수의 값에 따라 분기 처리하기

```js
switch(expression) {
    case value1:
        // value1 일 경우 실행
        break;
    case value2:
        // value2 일 경우 실행
        break;
    //...
    default:
        // 위 값들에 해당하지 않을 경우 실행
        break;
}
```

* default 구문을 생략하지 않는다.
* case 문의 마지막은 break 명령으로 끝난다.
* expression 과 case 의 값은 `===` 연산자로 비교한다.

```js
var day = new Date().getDay();
// 요일을 숫자로 변환(0은 일요일, 1은 월요일..., 6은 토요일)

switch (day) {
    case 1:
        console.log('월요일');
        break;
    case 2:
        console.log('화요일');
        break;
    case 3:
        console.log('수요일');
        break;
    case 4:
        console.log('목요일');
        break;
    case 5:
        console.log('금요일');
        break;
    case 0:
    case 6:
        console.log('주말/주일');
        break;
    default:
        console.log('요일이 아닙니다.');
}
```

### for 문

지정된 횟수만큼 반복 처리하기

```js
for (initialize; expession; update) {
    statements;
}

// 0부터 9까지 출력
for (var i = 0, total = 10; i < total; i++) {
    console.log(i);
}
```

```js
// 모든 li에 'on' 클래스 적용하기
// 태그 이름으로 엘리먼트를 찾을 때
// document.getElementsByTagName('태그명');
var objLi = document.getElementsByTagName('li');
for (var i = 0, total = objLi.length; i < total; i++) {
    objLi[i].className = 'on';
}
```

### for - in 문

객체의 프로퍼티를 나열하는 데 사용합니다.

```js
for(var propName in window) {
    console.log(propName);
}
```

```js
var human = {
    head: 1,
    hand: 2,
    leg: 2,
    think: function() {
        console.log('Think!');
    }
}

if (typeof Object.prototype.eat === 'undefined') {
    Object.prototype.eat = function() {
        console.log('Eat!');
    }
}

for (var i in human) {
    console.log(i, ': ', human[i]);
}
```

```js
var human = {
    head: 1,
    hand: 2,
    leg: 2,
    think: function() {
        console.log('Think!');
    }
}

if (typeof Object.prototype.eat === 'undefined') {
    Object.prototype.eat = function() {
        console.log('Eat!');
    }
}

for (var i in human) {
    if (human.hasOwnProperty(i)) {          // 인스턴스의 자체 프로퍼티만 출력
        console.log(i, ': ', human[i]);
    }
}
```

### while 문

조건에 따라 처리를 반복 실행하기

```js
while(expression) {
    statement;
}

// 1부터 10까지 출력
var i = 1;
while(i <= 10) {
    console.log('i: ' + i);
    i++;
}
```

> 무한루프 주의, i가 순환문 안에서 업데이트 되야한다.

### do-while 문

```js
do {
    // 순환문은 최소 한번은 실행됩니다.
    statement;
} while(expression);

// 'end'가 입력될 때까지 계속 입력창 띄우기
do {
    value = window.prompt('end가 입력될 때까지 계속 입력 받습니다.');
} while(value != 'end');
```

### break, continue

* break 문장은 switch나 순환문 안에서 사용할 수 있고, '이 코드 블록을 즉시 끝내라' 는 뜻 입니다.
* continue 문장은 순환문 안에서 사용할 수 있고, '다음 순환으로 이동하라' 는 뜻 입니다.

```js
// 배열 안에 5가 몇 번 인덱스에 있는지 구하기
var arr = [3, 4, 5, 1, 2, 6];
for (var i = 0, total = arr.length; i < total; i++) {
    console.log(i);
    if(arr[i] == 5) {
        console.log('5의 인덱스는 ' + i + '입니다.');
        break;
    }
}

// 배열에 공백문자가 있을 경우 건너뛰기
var step = ['사과를', '잘라서', '', '접시에 놓고', '', '먹어라!'];

for(var i = 0, total = step.length; i < total; i++) {
    if(step[i] === '') {
        continue;
    }
    console.log(step[i]);
}
```

*****

### 데이터 타입변환 연습

```js
// 데이터 타입변환
// 암시적(묵시적) 변환

var num = 23;
var str = "Hello~!!";
var str1 = "7";
var bool = true;

var numNum = num + num;
var numStr = num + str;
var numBool = num + bool;
var boolStr = bool + str;
var boolBool = bool + bool;

console.log('numNum : ', numNum, typeof numNum);
console.log('numStr : ', numStr, typeof numStr);
console.log('numBool : ', numBool, typeof numBool);
console.log('boolStr : ', boolStr, typeof boolStr);
console.log('boolBool : ', boolBool, typeof boolBool);

var numStrBool = num + str + bool;
var numBoolStr = num + bool + str;

console.log('numStrBool : ',numStrBool, typeof numStrBool);
console.log('numBoolStr : ',numBoolStr, typeof numBoolStr);

var numStr1Multi = num * str1;
var numBoolMulti = num * bool;
var numStrMulti = num * str;

console.log('numStr1Multi : ', numStr1Multi, typeof numStr1Multi);
console.log('numBoolMulti : ', numBoolMulti, typeof numBoolMulti);
console.log('numStrMulti : ', numStrMulti, typeof numStrMulti);
```

```js
// 데이터 타입 변환
// 명시적 변환

var num = 23;
var str = "7";
var bool = true;

var numToStr = String(num);
var numToStr1 = "" + num;
var numToStr2 = num.toString();

console.log('numToStr : ', numToStr, typeof numToStr);
console.log('numToStr1 : ', numToStr1, typeof numToStr1);
console.log('numToStr2 : ', numToStr2, typeof numToStr2);

var boolToNum = Number(bool);
var boolToNum1 = +bool

console.log('boolToNum : ', boolToNum, typeof boolToNum);
console.log('boolToNum1 : ', boolToNum1, typeof boolToNum1);

var strToNum = Number(str);
var strToNum1 = parseInt(str);
var strToNum2 = +str;

console.log('strToNum : ', strToNum, typeof strToNum);
console.log('strToNum1 : ', strToNum1, typeof strToNum1);
console.log('strToNum2 : ', strToNum2, typeof strToNum2);
```

> 단항 덧셈 연산자(+)는 Number() 함수와 같은 일을 합니다.

*****

### References

**MDN**

* https://developer.mozilla.org/ko/docs/Web/JavaScript

**생활코딩**

* https://opentutorials.org/course/743
* https://opentutorials.org/course/1375