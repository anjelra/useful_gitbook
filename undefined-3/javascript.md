---
description: 봐야할 사이트 정리 및 잊지 말아야 할 것을 정리
---

# javascript

### javascript 정리 &#x20;

### [https://learnjs.vlpt.us/](https://learnjs.vlpt.us/)

### 정규표현식&#x20;

{% embed url="https://hamait.tistory.com/342" %}

{% embed url="https://developer.mozilla.org/ko/docs/Web/JavaScript/Guide/%EC%A0%95%EA%B7%9C%EC%8B%9D" %}

### 자바스크립트 형변환

1. **암시적 변환**

&#x20;     자바스크립트 엔진이 필요에 따라 자동으로 데이터 타입을 변환시키는 것.

&#x20;  **2. 명시적 변환**

&#x20;    개발자가 의도를 가지고 데이터타입을 변환시키는 것.&#x20;

{% embed url="https://medium.com/gdana/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8%EC%9D%98-%ED%98%95%EB%B3%80%ED%99%98%EC%9D%80-%EB%91%90%EA%B0%80%EC%A7%80%EB%8B%A4-b46875be4a88" %}

### 얕은 복사(shallow copy)와 깊은 복사(deep copy)

{% embed url="https://brunch.co.kr/@kd4/87" %}

### es6 arrow function의 가장 큰 특징

* arrow function을 쓰게 되면 this가 살아있어서 밖에서 접근했던 this를 따로 선언해주지 않아도 물고 들어가는 특징이 있음.&#x20;
* arrow function은 생성자 함수로는 사용할 수 없다. 생성자 함수는 prototype 프로퍼티를 가지며 prototype 프로퍼티가 가리키는 프로토타입 객체의 constructor를 사용한다. 하지만 화살표 함수는 prototype 프로퍼티를 가지고 있지 않다.
* monogose의 스키마의 메소드를 선언할 때는 화살표 함수를 쓰면 안된다. 왜냐하면, 화살표 함수는 this를 가지고 있지 않기 때문이다.(bind를 따로 해주어야 한다.)

### es6 class&#x20;

{% embed url="https://beomy.tistory.com/15" %}

### array를 Object로 변환

* Obejct.entries()&#x20;

### Object를 array로 변환

{% embed url="https://codingcoding.tistory.com/1244" %}

### getter, setter

{% embed url="https://mygumi.tistory.com/161" %}

### hasOwnProperty는 프로토타입에 접근하지 않는다. for...in 문법은 열거가능한 프로토입에 접근한다. 따라서, for...in문 사용시, hasOwnProperty로 객체 자신의 프로퍼티 여부를 체크한 후 사용하는 것이 좋다.

{% embed url="https://mygumi.tistory.com/330" %}

### apply, call, bind

* call, apply 는 즉시 실행! 단, apply는 두번째 인자는 배열임.
* bind는 즉시 실행이 아
