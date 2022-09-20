---
description: 제 14장
---

# Null

### null 값 사용

null은 객체 속성이 아무런 값도 가지고 있지 않음을 명시적으로 나타날 때 사용할 수 있다. 속성을 처음 만들 때 값도 할당하는 것이 일반적이지만 값을 사용할 수 없는 경우도 있을 것이다. 이때는 null을 사용해 참조한 속성에 값이 없다는 것을 명시해야 한다.

```javascript
// foo 속성에 할당할 값이 아직 없어서 초기값을 null로 설정했다.
var myObjectObject = {foo: null};

console.log(myObjectObject.foo);    // 'null'이 기록된다.
```

* **null : 원래는 다른 값이 와야 하지만 아직 사용할 수 없는 경우에 넣어두는 값.**
* **undefined: 무언 결여되어 있음을 알려줄 때 자바스크립트가 사용하는 값.**

### typeof null == "object"

null 값을 가진 변수에 typeof 연산자를 사용해보면 'object'를 반환한다. 어떤 변수의 값이 null인지 정확히 하고 싶다면 등호를 사용하여 변수의 값이 null과 동일한지 살펴보는 것이 가장 좋다.

```javascript
var myObject = null;

console.log(typeof myObject);    // 'object'가 기록된다.
console.log(myObject === null);    // true가 나타난다.
```

**null값을 확인할 때는 항상 === 사용해야 한다. == 는 null과 undefined를 구별하지 못하기 때문이다.**

