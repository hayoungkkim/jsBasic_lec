RegExp 타입
=====

## 주요 정규 표현식 패턴

| 패턴            | 매칭하는 문자열           | first match             | all match                   |
| ------------- | ------------------ | ----------------------- | --------------------------- |
| xyz           | 'xyz' 라는 문자열       | a`xyz`bxyz              | a`xyz`b`xyz`                |
| ^who          | 앞부분이 일치            | `who` is who            | `who` is who                |
| who$          | 뒷부분이 일치            | who is `who`            | who is `who`                |
| .             | 임의의 1문자            | `r`egular               | `regular`                   |
| [oyu]         | o, y, u 중 1개       | H`o`w do you do?        | H`o`w d`o` y`ou` d`o`?      |
| [b-d]         | b~d 사이 1개          | a`b`cdef                | a`bcd`ef                    |
| [^b-d]        | b~d 이외의 1개         | `a`bcdef                | `a`bcd`ef`                  |
| on\|ues\|rida | on, ues, rida 중 하나 | M`on`day Tuesday Friday | M`on`day T`ues`day F`rida`y |
| a\*b          | a가 0 or more       | `aab`c abc bc           | `aab`c `ab`c `b`c           |
| a+b           | a가 1 or more       | `aab`c abc bc           | `aab`c `ab`c bc             |
| a?b           | a가 0 or 1          | a`ab`c abc bc           | a`ab`c `ab`c `b`c           |
| .{m} `.{5}`   | 임의문자 m개            | `12345`6789ab           | `123456789a`b               |
| [els]{1,3}    | e, l, s 중 최소1, 최대3 | in th`e` darkness       | in th`e` darkn`ess`         |
| [a-z]{3,}     | a~z 중 최소3          | One `two` three         | One `two` `three`           |

*****

| 패턴   | 매칭하는 문자열                                 |
| ---- | ---------------------------------------- |
| \w   | 대/소문자, 숫자, 언더스코어(\_) (Alpahnumeric + _ ) = `[A-z0-9_]` |
| \W   | 문자 이외에 일치(`[^/w]` 와 동일) = `[^A-z0-9_]`   |
| \d   | 숫자에 일치(`[0-9]` 와 동일)                     |
| \D   | 숫자 이외에 일치(`[^0-9]` 와 동일)                 |
| \n   | 개행에 일치                                   |
| \t   | 탭 문자에 일치                                 |
| \s   | 공백 문자에 일치                                |
| \S   | 공백 이외의 문자에 일치                            |

*****

### 정규표현식 인스턴스 프로퍼티

RegExp 인스턴스 프로퍼티는 패턴에 대한 정보를 포함합니다.

* lastIndex - 패턴 매칭을 어느 위치에서 시작할지 나타내는 정수 값입니다. 이 값은 항상 0에서 시작합니다.
* global - g 플래그가 설정되었는지 나태내는 불리언 값입니다.
* ignoreCase - i 플래그가 설정되었는지 나타내는 불리언 값입니다.
* multiline - m 플래그가 설정되었는지 나타내는 불리언 값입니다.
* source - 정규표현식을 생성한 문자엽입니다.

```js
var pattern = /\[bc\]at/i;

console.log(pattern.global);        // false
console.log(pattern.ignoreCase);    // true
console.log(pattern.multiline);     // false
console.log(pattern.lastIndex);     // 0
console.log(pattern.source);        // '\[bc\]at'
```

### 정규표현식 인스턴스 메서드

#### exec()

정규표현식 검색에 성공하면 배열을 반환하고 정규표현식 객체의 프로퍼티들을 업데이트 합니다.

```js
var text = 'mom and dad and baby',
    pattern = /mom (and dad (and baby)?)?/gi;

var matches = pattern.exec(text);

console.log(matches.index);     // 0
console.log(matches.input);     // 'mom and dad and baby'
console.log(matches[0]);        // 'mom and dad and baby'
console.log(matches[1]);        // 'and dad and baby'
console.log(matches[2]);        // 'and baby'
```

* 반환된 배열의 첫 번째 데이터는 정규표현식과 일치하는 문자열이고, 
* 다음 데이터들은 일치한 각각의 캡처그룹에 일치하는 문자열입니다.

정규표현식 검색에 실패하면 `null`을 반환합니다.

> 캡처그룹은 `()` 문자로 지정할 수 있므며, 괄호 사이에 존재하는 표현식을 통해 찾은 결과를 묶음으로 처리할 수 있도록 해줍니다.

#### test()

문자열이 패턴에 일치할 때는 true를 반환하고 그렇지 않을 때는 false를 반환합니다.

```js
regexObj.test(str);
```

```js
var text = '000-00-0000',
    pattern = /\d{3}-\d{2}-\d{4}/;
    
if(pattern.test(text)) {
    console.log('The pattern was matched');
}
```

*****

#### str.replace()

문자열 메서드에 정규표현식을 사용

```js
str.replace(regexp|substr, newSubstr|function);
```

```js
// str.replace(regexp, newSubstr)
// 문자열 전체, 대소문자 구분 X

var re = /apples/gi,
    str = 'Apples are round, and apples are juicy.';
    newstr = str.replace(re, 'oranges');
    
console.log(newstr);
```

```js
// str.replace(regexp, newSubstr)
// 문자열의 특수 파라미터 사용

var re = /(\w+)\s(\w+)/,
    str = 'John Snow',
    newstr = str.replace(re, '$2, $&, You know nothing $1');

console.log(newstr)
```

```js
// str.replace(regexp, function)
// 함수에서 특수 파라미터 사용

function replacer(match, p1, p2, p3, offset, string) {
    // p1 is nondigits([^\d]*),
    // p2 digits(\d*),
    // p3 non-alphanumerics([^\w]*)

    return [p1, p2, p3].join(' - ');
}

var newString = 'abc12345#$*%'.replace(/([^\d]*)(\d*)([^\w]*)/, replacer);
console.log(newString);  // abc - 12345 - #$*%
```

```js
// str.replace(regexp, function)

function styleHyphenFormat(propertyName) {
    function upperToHyphenLower(match, offset, string) {
        console.log(match, offset, string);
        return (offset ? '-' : '') + match.toLowerCase();
    }

    return propertyName.replace(/[A-Z]/g, upperToHyphenLower);
}

styleHyphenFormat('borderTop');     // border-top
```