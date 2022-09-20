---
description: 제 13장
---

# 원시 문자열, 숫자, 불리언값 다루기

### 원시/시터럴 값은 속성에 접근할 때 객체로 변환된다

문자열, 숫자, 불리언 리터럴은 속성과 함께 사용할 때(ex: ture.toString()) 객체처럼 다루어질 수 있다. 우리가 이러한 원시값의 속성에 접근하려 하면 자바스크립트는 원시값과 관련 있는 생성자를 사용해 래퍼 객체를 만들어 이 객체의 속성과 메소드를 사용하도록 한다. 그리고 속성에 접근한 후에는 만들었던 래퍼 객체를 버린다. 이러한 변환 덕분에 우리는 원시값이 마치 원부터 객체였던 듯한 코드를 작성할 수 있는 것이다. 코드에서 원시값을 객체처럼 다룰 때, 자바스크립트는 원시값을 객체로 변환하여 속성에 접근할 수 있도록 한 후, 속성값을 반환한 후에는 다시 원시값으로 되돌려 놓는다. 여기서 발생하는 일과 이때 자바스크립트가 하는 일은 정확히 이해하고 있어야 한다.

**문자열:**

```javascript
// 문자열 객체를 객체처럼 다루기.
var stringObject = new String('foo');
console.log(stringObject.length);    // 3이 기록된다.
console.log(stringObject('length'));    // 3이 기록된다.

// 문자열 리터럴/원시값은 이 값을 객체처럼 다룰 때 객체로 변환된다.
var stringLiteral = 'foo';
console.log(stringObject.length);    // 3이 기록된다.
console.log(stringObject['length']);    // 3이 기록된다.

console.log('bar'.length);    // 3이 기록된다.
console.log('bar'['length']);// 3이 기록된다.
```

**숫자:**

```javascript
// 숫자 객체를 객체처럼 다루기
var nubmerObject = new Number(1.10023);
console.log(nubmerObject.toFixed());    // 1이 기록된다.
console.log(nubmerObject['toFixed']());    // 1이 기록된다.

// 숫자 리터럴/원시값은 이 값을 객체처럼 다룰 때 객체로 변환된다.
var numberLiteral = 1.10023;
console.log(numberLiteral.toFixed());    // 1이 기록된다.
console.log(numberLiteral['toFixed']());    // 1이 기록된다.

console.log((1234).toString());    // '1234'가 기록된다.
console.log((1234)['toString']());    // '1234'가 기록된다.
```

**불리언:**

```javascript
// 불리언 객체를 객체처럼 다루기
var booleanObject = new Boolean(0);
console.log(booleanObject.toString());    // 'false'가 기록된다.
console.log(booleanObject['toString']());    // 'false'가 기록된다.

// 불리언 리터럴/원시값은 이 값을 객체처럼 다룰 때 객체로 변환된다.
var booleanLiteral = false;
console.log(booleanLiteral.toString());    // 'false'가 기록된다.
console.log(booleanLiteral['toString']());    // 'false'가 기록된다.

console.log((true).toString());    // 'true'가 기록된다.
console.log((true)['toString']());    // 'true'가 기록된다.
```

### 평소에는 원시 문자열, 숫자, 불리언값을 사용해라

**문자열, 숫자, 불리언 값을 표현하는 리터럴/원시값은 더 빠르게 코딩할 수 있고 보기에도 더 간결하다.**

그러니 가급적이면 리터럴값을 사용하자. 뿐만 아니라 값을 만드는 방법에 따라 typeof 연산자의 정확성이 달라질 수도 있다(리터럴과 생성자 사용의 차이).

```javascript
// 문자열, 숫자, 불리언 객체
console.log(typeof new String('foo'));    // 'object'가 기록된다.
console.log(typeof new Number(1));    // 'object'가 기록된다.
console.log(typeof new Boolean(true));    // 'object'가 기록된다.

// 문자열, 숫자, 불리언 리터럴/원시값
console.log(typeof 'foo');    // 'object'가 기록된다.
console.log(typeof 1);    // 'number'가 기록된다.
console.log(typeof true);    // 'boolean'가 기록된다.
```
