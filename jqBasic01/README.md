
jQuery Study Step01
=====

## jQuery

* 자바스크립트 라이브러리
* 간결하지만 강력한 코드(write less, do more.)
* 크로스 브라우징
* 다양한 플러그인 제공

> **jQuery가 주요 기능**
> HTML문서 탐색 및 조작, 이벤트 처리, 애니메이션 및 Ajax 통신의 효율적이고 크로스브라우징이 지원되는 API 제공

[jQuery API Documentation](http://api.jquery.com/)

*****

### jQuery(), $() 함수

`jQuery()`를 줄여서 `$()`로 사용(alias)

```js
// 동일한 코드
jQuery('div');
$('div');

jQuery.trim(value);
$.trim(value);
```

### 셀렉터(Selector)

**기본 셀렉터**

| 셀렉터 | 설명 | 예 |
| ----- | ----- | ----- |
| * | 모든 요소 | $('*') |
| #id | 아이디와 일치하는 요소 | $('#target') |
| element | 태그명과 일치하는 요소 | $('h1') |
| .className | 클래스명과 일치하는 요소 | $('.banner') |
| selector1, selector2, selector3 | 여러 요소를 동시에 찾을 때 ,(쉼표) 사용 | $('a, #wrapper, .on') |

**계층 셀렉터**

| 셀렉터 | 설명 | 예 |
| ----- | ----- | ----- |
| ancestor descendant | ancestor요소의 후손 요소들(descendant) | $('#me a') |
| parent > child | parent요소의 자식(child) | $('#me > div') |
| prev + next | prev요소의 다음 next요소 | $('#me + div') |
| prev ~ siblings | prev요소 이후 형제(siblings)요소 | $('#me ~ p') |

**기본 필터**

| 셀렉터 | 설명 | 예 |
| ----- | ----- | ----- |
| :animated | 애니메이션 중인 요소 | $('img:animated') |
| :first | 최소의 요소 구하기 | $('p:first') |
| :last | 마지막 요소 구하기 | $('p:last') |
| :not(selector) | 셀렉터에 일치하지 않는 요소 | $('p:not(.red)'), $('input:not(:checked)') |
| :even | 짝수 번째 요소(0 시작) | $('li:even') |
| :odd | 홀수 번째 요소(0 시작) | $('li:odd') |
| :eq(index) | index번째 요소(0 시작) | $('li:eq(3)') |
| :gt(index) | index 이후 요소(index 미포함) | $('li:gt(2)') |
| :lt(index) | index 이전 요소(index 미포함) | $('li:lt(2)') |

**속성 필터**

| 셀렉터 | 설명 | 예 |
| ----- | ----- | ----- |
| [attr] | 지정한 속성을 갖는 요소 | $('input[type]') |
| [attr = value] | 속성의 값이 value와 같은 요소 | $('input[type="text"]') |
| [attr != value] | 속성의 값이 value와 같지않은 요소 | $('input[type!="text"]') |
| [attr ^= value] | 속성의 값이 value로 시작하는 요소 | $('[lang^="en"]') |
| [attr $= value] | 속성의 값이 value로 끝나는 요소 | $('[lang$="kr"]') |
| [attr *= value] | 속성의 값이 value를 포함하는 요소 | $('[lang\*="ko"]') |

**폼 필터**

| 셀렉터 | 설명 | 예 |
| ----- | ----- | ----- |
| :enabled | `<input type="text" disabled="enabled">` | $('#target :enabled') |
| :disabled | `<input type="text" disabled="disabled">` | $('#target :disabled') |
| :checked | `<input type="checkbox" checked="checked">` | $('#target :checked') |
| :focus | 포커스가 있는 요소 구하기 | $('#target :focus') |

**기타 필터**

| 셀렉터 | 설명 | 예 |
| ----- | ----- | ----- |
| :first-child | 첫 번째 자식 요소 | $('div:first-child') |
| :last-child | 마지막 자식 요소 | $('div:last-child') |
| :hidden | 숨김상태의 요소 | $('li:hidden') |
| :visible | 표시상태의 요소 | $('li:visible') |
| :empty | 자식요소를 갖지 않는 요소 | $('div:empty') |
| :has(selector) | 셀렉터와 일치하는 요소를 가지고 있는 요소 | $('div:has(a)') |

* [Selectors | jQuery API Documentation](http://api.jquery.com/category/selectors/)
* [jQuery Selectors](https://www.w3schools.com/jquery/jquery_ref_selectors.asp)
* [Try jQuery Selector](https://www.w3schools.com/jquery/trysel.asp)

> **셀렉터의 선택**
> jQuery 셀렉터 선택은 페이지의 성능을 개선하는데 큰 역할을 할 수 있습니다. 일반적으로 다음을 고려해서 선택하는 것이 좋습니다.
> 1. #id(id값으로 검색), element(요소명으로 검색)
> 2. .class(class 속성으로 검색)
> 3. 1, 2, 4번 이외의 셀렉터
> 4. jQuery 확장 셀렉터(jQuery Extensions Selector)
>
> `1`은 내부적으로 브라우저 표준 `getElementById`, `getElementsByTagName` 메서드로 대체되므로 모든 환경에서 빠르게 동작합니다.
> `2`도 내부적으로 `getElementsByClassName`, `querySelectorAll` 메서드로 대체되어 빠르지만 IE 구버전에서는 성능이 떨어질 수 있습니다.
> `4`는 jQuery가 항상 자체 해석을 하기 때문에 늘 속도가 떨어집니다.

*****

### 탐색

| 메서드 | 설명 |
| ----- | ----- |
| .eq(index) | 선택한 컬렉션 중 index에 해당하는 엘리먼트 |
| .filter(expr) | 선택한 컬렉션 중 표현식과 일치하는 엘리먼트, 표현식에는 selector, function, element, jQuery 객체가 올수 있습니다. |
| .first() | 선택한 컬렉션 중 첫 번째 엘리먼트 |
| .has(selector) | 선택한 컬렉션 중 selector 항목을 가지고 있는 엘리먼트 |
| .is(selector) | 선택한 컬렉션 중 selector 항목을 가지고 있는 엘리먼트 |
| .last() | 선택한 컬렉션 중 마지막 엘리먼트 |
| .not(expr) | 선택한 컬렉션 중 표현식과 일치하지 않는 엘리먼트 |
| .children([selector]) | 선택한 엘리먼트의 자식 중 selector에 해당하는 엘리먼트 |
| .closest(selector) | 선택한 엘리먼트의 가장 가까운 조상 중 selector에 해당하는 엘리먼트 |
| .find(selector) | 선택한 엘리먼트의 selector에 해당하는 후손 엘리먼트 |
| .next([selector]) | 선택한 엘리먼트의 selector에 해당하는 다음 형제 엘리먼트 |
| .prev([selector]) | 선택한 엘리먼트의 selector에 해당하는 이전 형제 엘리먼트 |
| .parent([selector]) | 선택한 엘리먼트의 selector에 해당하는 부모 엘리먼트 |
| .siblings([selector]) | 선택한 엘리먼트의 selector에 해당하는 형제 엘리먼트(자신 제외) |

### 스타일(Style)

#### css 값 가져오기, 설정하기

* .css(propertyName)
* .css(propoertyName, value)
* .css({prop1: value1, prop2: value2, ...})

```js
var sBgcolor = $('div').css('backgroundColor');
$('div').css('background-color', '#ff0000');
$('div').css({'margin': '10px', 'padding': '5px', 'color': '#993399'});
```

* .width()
* .height()
* .width(value)
* .height(value)

```js
var nDivWidth = $('div').width();
$('div').width(300);
$('div').width('100px');
$('div').height('+=100');
```

### 속성(Attribute)

#### 요소의 속성 값 가져오기, 적용하기, 제거하기

* .attr(attributeName)
* .attr(attributeName, value)
* .removeAttr(attributeName)

```js
var sSrcPath = $('img').attr('src');
$('img').attr('src', 'logo.png');
$('input').removeAttr('title');
```

#### 요소의 property 값 가져오기, 적용하기

* .prop(propertyName)
* .prop(propertyName, value)

```js
var bIsChecked = $('input[type="checkbox"]').prop('checked');
$('input[type="checkbox"]').prop('checked', true);
```

> attr() / prop()
>
> ```html
> <a href="#content1" id="anchor1"></a>
> <input type="checkbox" id="checkbox1">
> <input type="checkbox" id="checkbox2" checked>
> ``` 

>```js
> var welLink = $('#anchor1'),
>     welCheck1 = $('#checkbox1'),
>     welCheck2 = $('#checkbox2');
>
> console.log('anchor prop: ', welLink.prop('href'));
> console.log('anchor attr: ', welLink.attr('href'));
>
> console.log('checkbox1 prop: ', welCheck1.prop('checked'))
> console.log('checkbox1 attr: ', welCheck1.attr('checked'))
>
> console.log('checkbox2 prop: ', welCheck2.prop('checked'))
> console.log('checkbox2 attr: ', welCheck2.attr('checked'))
> ```
>
> attr()은 html attribute 를 다루고, prop()은 javascript dom 객체의 property 를 다룹니다.

#### 폼 요소 값 가져오기, 적용하기

* .val()
* .val(value)

```js
var sValue = $('input[type="text"].val()');
$('input[type="text"]').val('This is Value!');
```

### 조작(Manipulation)

#### 클래스 속성(Class Attribute)

**클래스 값 추가, 삭제, 토글**

* .addClass(className)
* .removeClass(className)
* .toggleClass(className)

```js
$('div').addClass('on');
$('div').removeClass('on');
$('div').toggleClass('on');
```

**해당 클래스를 가지고 있는지 판단**

* .hasClass(className)

```js
if($('#target').hasClass('on') {
    // ...
})
```

**타겟 외부에 DOM 추가, 제거**

* .wrap(wrappingElement)
* .unwrap()

```js
$('.inner').wrap('<div class="outer"></div>');
$('.inner').unwrap();
```

**타겟 앞, 뒤에 DOM 추가하기

* .before(content)
* .after(content)

```js
$('.middle').before('<p>before</p>');
$('.middle').after('<p>after</p>');
```

* .insertBefore(target)
* .insertAfter(target)

```js
$('<p>before</p>').insertBefore('.middle');
$('<p>after</p>').insertAfter('.middle');
```

**타겟 내부의 처음, 마지막에 DOM 추가하기

* .prepend(content)
* .append(content)

```js
$('.outer').prepend('<p>test</p>');
$('.outer').append('<p>test</p>');
```

* .prependTo(target)
* .appendTo(target)

```js
$('<p>test</p>').prependTo('.outer');
$('<p>test</p>').appendTo('.outer');
```

**타겟 내부의 html 가져오기, 설정하기**

* .html()
* .html(htmlString)

```js
var sHtmlString = $('div').html();
$('div').html('<p>new content <span class="on">added</span></p>');
```

**타겟 내부에 text 가져오기, 설정하기**

* .text()
* .text(text)

```js
var sText = $('div').text();
$('div').text('<p>new content <span class="on">added</span></p>');
```

**타겟 복제하기**

* .clone()

```js
$('.hello').clone().appendTo('.goodbye');
```

**타겟 내부 비우기**

* .empty()

**타겟 제거하기**

* .remove()
* .detach()