---
description: 제 15장
---

# undefined

### undefined 값

1. 선언한 변수가 아무런 값도 가지고 있지 않은지 확인할 때 사용한다.
2. 접근한 객체의 속성이 정의되지 않았으며 프로토타입 체인에서도 찾을 수 없는지 확인할 때 사용한다.

```javascript
var initializedValiable;

console.log(initializedValiable);    // undefined가 기록된다.
console.log(typeof initializedValiable);    // 자바스크립트가 undefined를 반환하는지 확인.

var foo = {};

console.log(foo.bar);    // foo 객체에는 bar 속성이 없으므로 undefined가 기록된다.
console.log(typeof foo.bar);    // 자바스크립트가 undefined를 반환하는지 확인.
```

### 자바스크립트 ECMAScript 3 이상에서 undefined는 전역 변수로 선언된다

```javascript
// undefined가 전역 속성인지 확인
console.log(undeifned in this);    // true가 기록된다.
```

