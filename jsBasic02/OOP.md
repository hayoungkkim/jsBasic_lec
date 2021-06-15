Javascript 객체 지향 프로그래밍
=====

ECMAScript 에서는 객체를 "프로퍼티의 순서 없는 컬렉션이며, 각 프로퍼티의 값은 원시 값이나 객체, 함수를 포함한다" 라고 정의합니다.

객체는 (특별한 순서가 없는)이름-값 쌍의 그룹이며, 각 값은 데이터나 함수가 될 수 있습니다.

*****

모든 객체는 참조 타입을 바탕으로 생성되는데, 이 바탕이 되는 타입은 네이티브 타입일 수도 있고 개발자가 정의한 타입일 수도 있습니다.

**자바스크립트에서 객체를 생성하는 방법**

* 객체리터럴
* 생성자 함수(`new Object()`)

```js
// 객체 리터럴
var obj = {}

// Object() 생성자 함수
var obj = new Object();
```

*****

## 객체를 만드는 가장 단순한 방법

Object 의 인스턴스를 만들고 여기에 프로퍼티와 메서드를 추가하는 방법입니다.

```js
var animal = new Object();
// var animal = {};

animal.name = 'MS';
animal.age = 21;
animal.job = 'Too much talker';

animal.sayName = function() {
    console.log(this.name);
}

var animal2 = {
    name: 'MS2',
    age: 21,
    job: 'TMT',
    
    sayName: function() {
        console.log(this.name);
    }
}

animal.sayName();
```

객체 하나를 생성할 때는 편리하지만, 객체를 여러개 만들 때는 중복된 코드를 매우 많이 써야하는 문제점이 있습니다. 이 문제를 해결하기 위해 함수를 만들어 객체를 생성합니다.

*****

## 객체 생성

### 팩터리 패턴

팩터리 패턴은 객체를 생성하는 과정을 함수로 추상화하는 것입니다.

> 추상화의 예 : 같은 일을 하는 코드의 공통점을 모아 함수를 만드는 것

```js
function createAnimal(name, age, job) {
    var o = new Object();
    o.name = name;
    o.age = age;
    o.job = job;
    o.sayName = function() {
        console.log(this.name);
    };

    return o;
}

var animal1 = createAnimal('MS', 21, 'TMT');
var animal2 = createAnimal('JY', 22, 'Smart');
```

팩터리 패턴의 문제점은 타입이 많아지면, 생성한 객체가 어떤 타입이지 알 수가 없다는 것입니다.

*****

### 생성자 패턴

`Object()` 와 `Array()`는 실행 환경에서 자동으로 만들어지는 네이티브 생성자입니다.
커스텀 생성자를 만들어서 원하는 타입의 객체를 만들고 필요한 프로퍼티와 메서드를 직접 정의할 수 있습니다.

```js
function Animal(name, age, job) {
    this.name = name;
    this.age = age;
    this.job = job;
    
    this.sayName = function() {
        console.log(this.name);
    }
}

var animal1 = new Animal('MS', 21, 'TMT');
var animal2 = new Animal('JY', 22, 'Smart');
```

팩터리 함수와 다른 점

1. 명시적으로 객체를 생성하지 않습니다.
2. 프로퍼티와 메서드는 `this` 객체에 직접적으로 할당됩니다.
3. `return` 문이 없습니다.

생성자임을 나타내기 위해서 관용적으로 함수 이름의 첫 글자를 대문자로 합니다.

새 인스턴스를 만들 때는 `new` 연산자를 사용합니다.
생성자를 `new` 연산자와 같이 호출하면 내부적으로 다음과 같은 과정이 이루어 집니다.

1. 객체를 생성합니다.
2. 생성자의 `this` 값에 새 객체를 할당합니다. 따라서 `this`가 만들어진 새 객체를 가리킵니다.
3. 생성자 내부 코드를 실행합니다.(객체에 프로퍼티를 추가합니다.)
4. 새 객체를 반홥니다.

> `new` 없이 생성자 함수를 사용하면?

일반적인 함수와 똑같이 동작합니다.

```js
// 생성자로 사용
var animal = new Animal('MS', 21, 'TMT');
animal.sayName();   // 'MS'

// 함수로 호출
Animal('JY', 22, 'Smart');
sayName();          // 'JY'
window.sayName();   // 'JY'
```

#### 생성자 패턴의 문제점

인스턴스마다 메서드가 생성된다는 점(비효율성)
animal1, animal2 모두 이름이 같은 `sayName()` 이라는 메서드가 있지만 Function 타입의 서로다른 인스턴스 입니다.

```js
console.log(animal1.sayName == animal2.sayName);    // false
```

*****

### 프로토타입 패턴과 조합

* 모든 함수를 `prototype` 프로퍼티를 가집니다.
* 이 프로퍼티는 해당 참조타입의 인스턴스가 가져야 할 프로퍼티와 메서드를 담고 있는 객체입니다.
* `prototype` 객체는 생성자가 호출될 때 생성되는 객체의, 즉 인스턴스의 문자 그대로 프로토타입입니다.
* `prototype`의 프로퍼티와 메서드는 인스턴스 전체에서 공유됩니다.

#### 프로토타입은 어떻게 동작하는가?

* 함수가 생성될 때 마다 프로토타입 객체가 생성 됩니다.
* 모든 프로토타입은 `constructor` 프로퍼티를 갖고, 이 프로퍼티는 해당 프로토타입이 프로퍼티로서 소속된 함수를 가리킵니다.

```js
function Animal() {}

console.log(Animal.prototype.constructor);  // Animal 을 가리킵니다.
```

* 생성자를 호출해서 인스턴스를 생성할 때마다 해당 인스턴스 내부에는 생성자의 프로토타입을 가리키는 포인터가 생성됩니다. `__proto__` 비공식 프로퍼티
* 인스턴스와 연결되는 것은 생성자의 프로토타입 입니다. 생성자 자체가 아닙니다.

```js
function Animal(name, age, job) {
    this.name = name;
    this.age = age;
    this.job = job;
}

Animal.prototype.sayName = function() {
    console.log(this.name);
}
    
var animal1 = new Animal('MS', 21, 'TMT');
var animal2 = new Animal('JY', 22, 'Smart');

console.log(animal1.sayName());
console.log(animal2.sayName());
console.log(animal1.sayName == animal2.sayName);
```

> 생성자 - 프로토타입 - 인스턴스의 관계

#### 네이티브 객체의 프로토타입

```js
console.log(String.prototype);

String.prototype.isStartWith = function(text) {
    return this.indexOf(text) == 0;
}

var test = 'Hello world!';
console.log(test.isStartWith('Hello'));
```

생성자/프로토타입 패턴은 ECMAScript 에서 커스텀 참조타입을 정의할 때 가장 널리 사용되는 방법입니다.

*****

#### 정적멤버(Static Member)

* 함수자체도 객체이므로 생성자 함수객체의 직속으로 프로퍼티를 추가할 수 있습니다.
* 생성자의 인스턴스에서는 접근할 수 없습니다.
* 일반적으로 유틸리티적인 기능을 구현할 때 사용합니다.

```js
function SEUI() {}

SEUI.START_YEAR = 2014;
SEUI.getPeriod = function() {
    var nYear = new Date();
    return nYear.getFullYear() - SEUI.START_YEAR;
}

console.log(SEUI.getPeriod());
```

#### 상속

```js
function Animal() {}

Animal.prototype.eat = function(food) {
    console.log(food + ' 를 우걱우걱');
}

function Shiva() {}
Shiva.prototype = new Animal();         // Animal을 상속한 시바

Shiva.prototype.say = function() {
    console.log('월월');
}

var sb = new Shiva();
console.log(sb.say());
console.log(sb.eat('지지'));
console.log(sb);
```

#### 전용멤버(Private Member)

* 정보/절차 보안
* 클로저

```js
function Animal(name, age, secret) {
    this.name = name;
    this.age = age;
    
    var _secret = secret;
    
    this.getSecret = function() {
        console.log(_secret);
    }
}

Animal.prototype.method = function () {}

var animal = new Animal('MS', 21, 'Handsome');

animal._secret;
animal.getSecret();
```