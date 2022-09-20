---
description: 제 7장
---

# 스코프와 클로저

### 자바스크립트의 스코프

자바스크립트에서 **스코프는 코드가 실행되는 컨텍스트이며, 전역 스코프, 지역 프코프, eval 스코프 크게 세 종류로 구분**된다. 함수 내에서 var를 사용해 정의된 코드는 지역 스코프에서만 유효하다. 다시 말해, 해당 함수 내에서 정의된 중첩 또는 자식 함수를 비롯해 해당 함수 내부에서만 사용할 수 있다.

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

자바스크립트에서는 var 키워드 없이 변수를 선언하면(설령 함수 스코프에서 선언했다고 하더라도) 지역 스코프가 아닌 전역 스코프에 변수가 추가된다.

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

따라서 함수 내에서 변수를 선언할 때에는 항상 var를 사용해야 한다. 그렇지 않으면 스코프 때문에 혼란스러워지는 문제가 발생할 수 있다.

### 스코프 체인(문법적 스코프)

자바스크립트는 변수를 찾을 때 스코프의 계층 구조에 기반한 검색 체인을 거슬러 올라가며 추적한다.

```javascript
var sayHiText = 'howdy';

var func1 = function() {
    var func2 = function() {
        console.log(sayHiText);
    }();
}();
```

func2 함수 스코프 내에 포함되어 있지 않은 sayHiText의 값을 어떻게 찾았을까?

1. func2함수에서 sayHiText라는 변수를 찾는다.
2. 없으면 func2의 부모 함수인 func1에서 다시 검색한다.
3. func1 스코프에서도 sayHiText를 찾지 못하면 func1 함수는 부모 함수가 없으므로 전역 스코프에서 sayHiText를 검색하고, sayHiText를 발견하면 이 값을 func2로 전달한다.
4. 만약, sayHiText가 전역 스코프에도 정의되어 있지 않았다면 자바스크립트는 undefined를 반환했을 것이다.

```javascript
var x = 10;
var foo = function() {
    var y = 20;
    var bar = function() {
        var z = 30;
        console.log(z + y + x);
    }();
}();

foo();    // 60이 기록된다.
```

**스코프 체인은 프로토타입 체인과 크게 다르지 않다. 두 방법 모두 시스템적 계층적인 위치를 검색하여 원하는 값을 구한다.**

### **스코프 체인을 검색할 때는 가장 처음 발견한 값을 반환한다.**

```javascript
var x = false;
var foo = function() {
    var x = false;
    bar = function() {
        var x = true;
        console.log(x);
    }();
};

foo();    // true가 기록된다.
```

**변수를 검색할 때는 스코프 체에서 가장 가까운 스코프부터 검색하며, 값을 찾으면 상위 스코프에 같은 이름의 값이 있더라도 찾은 값을 반환하고 검색을 종료한다.**

### **스코프는 함수를 정의할 때 결정된다**

스코프 체인은 함수를 실행한 위치가 아닌 정의한 위치에 의해 결정된다. 이를 가리켜 문법적 스코핑(lexical scoping)이라고도 한다.&#x20;

스코프 체인은 함수를 호출하기 전에 이미 만들어지며, 이 덕에 클로저(closure)를 만들 수 있다. 예를 들어, 다른 함수 내부에 정의되어 있다가 전역 스코프로 반환된 함수가 있다고 가정해 볼 때, 반환된 함수는 전역 스코프에 있더라도 스코프 체인을 통해 부모 함수에 여전히 접근할 수 있다.

**아래의 코드를 보면, 우리는 익명 함수를 반환하는 parentFunction이라는 함수를 정의한 후 전역 스코프에서 이 함수를 호출할 것이다. 반환된 익명 함수는 parentFunction 내부에서 정의되었기 문에 실행될 때 parentFunction의 스코프에 접근할 수 있다. 이를 가리켜 클로저라 부른다.**

```javascript
var parentFunction = function() {
    var foo = 'foo';
    return function() {      // 반환할 익명 함수
        console.log(foo);    // 'foo'가 기록된다.
    }
}

// nestedFunction은 parentFunction 함수에서 반환된 익명 함수를 참조한다.
var nestedFunction = parentFunction();

nestedFunction();    // 반환된 함수는 스코프 체인을 통해 foo에 접근할 수 있으므로 여기서는 foo가 기록된다.
```

**스코프 체인은 정의할 때,  문자 그대로 코드를 작성할 때 정해진다. 함수를 어느 곳에서 사용해도 스코프 체인은 변하지 않는다.**

### **스코프 체인이 클로저를 만든다**

클로저는 이 장에서 배웠던 스코프 체인 및 스코프 검색에 대한 내용만 가지고도 충분히 이해할 수 있다.&#x20;

```javascript
var countUpFromZero = function() {
    var count = 0;
    return function() {    // countUpFromZero가 참조할 중첩 함수를 반환한다.
        return ++count;    // count는 스코프 체인 위, 정확히 말해 부모 함수에 정의되어 있다.
    }
}();

console.log(countUpFromZero());    // 1이 기록된다.
console.log(countUpFromZero());    // 2이 기록된다.
console.log(countUpFromZero());    // 3이 기록된다.
```

countUpFromZero 함수는 실행할 때마다 자신을 포함했던 부모 함수의 스코프에 접근할 수 있다. 스코프 체인을 사용한 이 기법은 클로저의 사례 중 하나다.
