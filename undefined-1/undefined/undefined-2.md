---
description: 제 7장
---

# 스코프와 클로저

### 자바스크립트의 스코프

자바스크립트에서 스코프는 코드가 실행되는 컨텍스트이며, 전역 스코프, 지역 프코프, eval 스코프 크게 세 종류로 구분된다. 함수 내에서 var를 사용해 정의된 코드는 지역 스코프에서만 유효하다. 다시 말해, 해당 함수 내에서 정의된 중첩 또는 자식 함수를 비롯해 해당 함수 내부에서만 사용할 수 있다.

```javascript
var foo = 0;    // 전역 스코프

console.log(foo);    // 0이 기록된다.

var myFunction = function() {
    var foo = 1;         // 지역 스코프
    console.log(foo);    // 1이 기록된다.
    
    var myNestedFunction = function() {
        var foo = 2;    // 지역 스코프
        console.log(foo);    // 2이 기록된다.
    }();
}();

eval('var foo = 3; console.log(foo);');    // eval() 스코
```

### 자바스크립트에는 블록 스코프가 없다

자바스크립트에서 조건문과 반복문은 스코프를 만들지 않으므로 조건문과 반복문 사이에도 변수를 서로 재정의할 수 있다. 자바스크립트에는 블록 스코프가 없기 때문에 프로그램을 진행하면 foo의 값도 변경된다. 자바스크립트에는 함수, 전역, eval 스코프만 있다.

```javascript
var foo = 1;    // foo = 1

if (true) {
    foo = 2;
    for (var i = 3; i <= 5; i++) {
        foo = i;    // foo = 순서대로 3, 4, 5
        console.log(foo);    // 순서대로 3, 4, 5가 각각 기록된다.
    }
}
```

### 함수 내에서 변수 선언 시 var를 사용해 스코프 문제 피하기

자바스크립트에서는 var 키워드 없이 변수를 선언하면\(설령 함수 스코프에서 선언했다고 하더라도\) 지역 스코프가 아닌 전역 스코프에 변수가 추가된다.

```javascript
var foo = function() {
    var boo = function() {
        bar = 2;    // var을 사용하지 않았으므로 bar는 전역 스코프 window.bar로서 정의된다.
    }();
}();

console.log(bar);    // bar는 전역 스코프에 있으므로 2가 기록된다.

// 반대로
var foo = function() {
    var boo = function() {
        var doo = 2;
    }();
}();

console.log(doo);    // doo는 boo 함수 스코프 내에만 있으므로 에러가 발생하여 undefined가 기록된다.
```

