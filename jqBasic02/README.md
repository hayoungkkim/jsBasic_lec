
jQuery Study Step02
=====

## jQuery Event

### 이벤트 핸들러

#### 이벤트 등록하기(이벤트 핸들러/리스러 연결)

* .on(events, handler)
* .on(events [, selector], handler)
* .on(events [, selector]  [, data], handler)

```js
$('#target ul li').click(function() { /* ... */ });
$('#target ul li').on('click', function() { /* ... */ });

// 이벤트 위임(delegate)
$('#target ul').on('click', 'tr', function() { /* ... */});

// 데이터 전달하기
$('#target ul li').on('click', {foo: 'bar'}, function() { /* ... */});
```

**이벤트 등록 후 한번만 실행하기**

* .one(events', handler)

```js
$('#target ul li').one('click', function() { /* ... */});
```

#### 이벤트 삭제하기(이벤트 핸들러 제거하기)

* .off()
* .off(events)

```js
$('#target ul li').off();
$('#target ul li').off('click');
```

#### 이벤트 네임스페이스(namespace)

```js
$('#list a').on('click.myNamespace', function() {
    // ...
})
```

#### 이벤트 동시 등록하기

```js
$('#list a').on('click focus', function() {
    // ...
})
```

#### 이벤트 발생시키기

* .trigger(eventType [, extraParameters])

```js
// 이벤트 등록하기
$('#target ui li').on('click', function() {
    console.log("Click!");
})

// 이벤트 발생시키기
$('#target ui li').trigger('click');
```

#### 커스텀 이벤트

```js
// 이벤트 등록
$('#target ul li').on('afterShow', function() {
    console.log('임의의 이름으로 이벤트 등록');
});

// 이벤트 발생시키기
$('#target ul li').trigger('afterShow');
```

### 로딩

#### DOM이 준비되었을 때

* .ready(handler)

```js
jQuery(document).ready(function() {
    // ...
});

$(document).ready(function() {
    // ...
});

$(function () {
    // ...
});
```

#### 모든 요소의 로드가 완료되었을 때

* .load(handler)

```js
$(window).load(function() {
    // ...
});

$('img').load(function() {
    // ...
})
```

> ```js
> window.onload = function() { /* ... */ }
> $(window).on('load', function() { /* ... */});
> ```

### 브라우저 이벤트

#### 브라우저 리사이즈 발생 시

* .resize(handler)

```js
$(window).resize(function() {
    // ...
});
```

#### 스크롤 발생 시

* .scroll(handler)

```js
$(window).scroll(function() {
    // ...
});

$('#target').scroll(function() {
    // ...
});
```

#### 에러 발생 시

* .error(handler)

```js
$('img').on('error', function() {
    // ...
})
```

#### 마우스 이벤트

* .click()
* .dbclick()
* .mouseenter()
* .mouseleave()
* .mousehover()
* .mousemove()
* .mousedown()
* .mouseup()

#### 키보드 이벤트

* .keydown()
* .keypress()
* .keyup()

#### 폼 이벤트

* .blur()
* .change()
* .focus()
* .submit()

*****

### 이벤트 객체

* event.target
* event.currentTarget
* event.type
* event.data
* event.pageX
* event.pageY
* event.preventDefault()
* event.stopPropagation()

```js
$("#target a").on("click", function (e) {
    e.preventDefault();
    console.log(e.type, e.currentTarget, e.pageX, e.pageY);
});
```