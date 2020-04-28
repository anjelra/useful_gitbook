---
description: 제 5장
---

# 머리/전역 객체

### 머리 객체의 사용\(머리 객체는 window!\)

자바스크립트 코드는 반드시 객체에 포함되어 있어야 한다. 예를 들어, 웹 브라우저 환경에서 자바스크립트를 사용하는 경우, 자바스크립트는 window 객체 안에 포함되고 그 안에서 실행된다. 이 때 window 객체를 가리켜 "머리 객체" 또는 "전역 객체"라 부른다. 자바스크립트 언어라면 무엇이든 이러한 머리 객체를 하나씩 사용해야 한다.

자바스크립트는 머리 객체를 만들어 사용자가 정의한 코드를 캡슐화하거나 자바스크립트에 내장된 네이티브 코드를 감싼다. 또한 자바스크립트는 사용자 정의 코드의 실행 영역을 머리 객체 내부로 제한한다. 

### 머리 객체에 포함된 전역 함수

자바스크립트가 언제든 사용할 수 있도록 미리 준비해 둔 함수 또는 \(머리 객체의\) 메소드라 할 수 있다.

* decodeURI\(\)
* decodeURIComponent\(\) -&gt; 암호화된 URI 컴포넌트에서 각각의 이스케이프 시퀀스\(확장 문자열\)를 자신을 나타내는 문자로 바꿉니다
* encodeURI\(\)
* encodeURIComponent\(\)
* eval\(\)
* isFinite\(\) -&gt; 숫자가 유한수인지 판별하기 위해 사
* isNaN\(\)
* parseFloat\(\)
* parseInt\(\)

### 머리 객체 vs 전역 속성, 전역 변수

머리 객체는 모든 객체를 포함하고 있는 객체다. 전역 속성이나 전역 변수라는 용어는 머리 객체에 직접적으로 포함되어 있는 값을 가리킬 때 사용되며, 다른 객체의 특정한 스코프에 포함된 값에는 사용하지 않는다.

```javascript
var foo = 'bar';    // foo는 전역 객체이자 window 머리 객체의 속성이다.

var myApp = function() {    // 함수는 스코프를 만든다.
    var run = function() {
        // bar가 기록된다. 스코프 체인을 통해 머리 객체에서 foo의 값을 찾은 것이다.
        console.log(foo);
    }
}

myApp();
```

만약 foo 속성을 전역 스코프가 아닌 곳에 둔다면 console.log 함수는 아마도 undefined를 기록할 것이다. 

```javascript
var myFunction = function() {
    var foo = 'bar';
}

var myApp = function() {    // 함수는 스코프를 만든다.
    var run = function() {
        // foo는 전역 스코프에 없으므로 undefined 기
        console.log(foo);
    }
}
```

위와 같은 특성 때문에 우리는 브라우저 환경에서 어디든 글로벌 속성 메소드\(예: window.alert\(\)\)을 호출할 수 있는 것이다. 전역 스코프에 있는 것은 어떤 스코프에서도 사용 가능하다. 그러므로 이들을 가리켜 "전역 변수" 또는 "전역 속성"이라고 부른다.

### 머리 객체 참조하기

1. 간단히 머리 객체의 이름을 참조하는 것이다.\(예 웹 브라우저에서는 window를 사용한다.\)
2. 전역 스코프에서 this를 사용하는 것이다.

```javascript
var foo = 'bar';

windowRef1 = window;
windowRef2 = this;

console.log(windowRef1, windowRef2);    // window 객체의 참조가 기록된다.

console.log(windowRef1.foo, windowRef2.foo);    // 'bar', 'bar'가 기록된다.
```

### 머리 객체는 생략될 수 있다

window.alert\(\)이라고 쓰지 않고 alert\(\)이라고 쓸 수 있는 것처럼 머리 객체는 생략이 가능하다.

```javascript
var foo = {    // 여기서는 window 가 생략된 셈이다. 실제로는 window.foo다.
    fooMethod: function() {
        alert('foo' + 'bar');    // 여기서도 window가 생략. window.alert
        window.alert('foo' + 'bar');
    }
};

foo.fooMethod();    // 여기서는 window가 생략. 실제로는 window.foo.fooMethod()
```

**머리 객체는 스코프 체인의 종점에 있기 때문에 명시적으로 포함하지 않고 생략할 수 있다.**

