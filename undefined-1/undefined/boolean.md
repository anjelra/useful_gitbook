---
description: 제 12장
---

# Boolean\(\)

### Boolean\(\) 객체의 사용

```javascript
// new 키워드와 Boolean() 생성자를 사용해 불리언 객체 만들기.
var myBoolean1 = new Boolean(false);   
console.log(ypteof myBoolean1);     // 'object'가 기록됨.

var myBoolean2 = Boolean(0);
console.log(typeof myBoolean2);    // 'boolean'이 기록됨.

// 리터럴/원시 불리언값 만들기
var myBoolean3 = false;
console.log(typeof myBoolean3);    // 'boolean'이 기록됨.
console.log(myBoolean1, myBoolean2, myBoolean3);    // false{} false false가 반환됨.
```

### Boolean\(\) 매개변수

Boolean\(\) 생성자 함수에는 불리언값으로 변환 가능한 한 개의 매개변수를 전달할 수 있다. 자바스크립트 값 중 0, -0, null, false, NaN, undeifiend, 빈 문자열\(""\)은 false로 반환. 그 밖의 값은 true로 반환된다.

```javascript
// Boolean()에 전달된 매개변수 = 0 = false, 따라서 foo = false
var foo = new Boolean(0);
console.log(foo);

// Boolean()에 전달된 매개변수 = Math = true, 따라서 bar = true
var bar = new Boolean(Math);
console.log(bar);
```

**Boolean\(\) 생성자와 new 키워드를 사용해 만든 인스턴스는 실제로는 복합 객체를 만들어낸다. 따라서 typeof  연산자와 관련한 문제가 발생할 수 있으므로 가능하다면 불리언값을 만들 때는 Boolean\(\) 생성자를 명시적으로 사용하지 않는 것이 좋다\(대신 리터럴/원시값을 권장한다\). typeof 연산자를 사용하면 원시값에 대해서는 'boolean'이라고 기대했던 대로 알려주지만 객체에 대해서는 'object\(객체\)'라고 알려준다. 게다가 리터럴/원시값은 코드를 작성하는 노력도 줄여준다는 장점이 있다.**

### **Boolean\(\)의 속성과 메소드**

#### **속성**

* prototype ****

### Boolean 객체 인스턴스의 속성과 메소드

#### 인스턴스 속성

* constructor

#### 인스턴스 메소드

* toSource\(\)
* toString\(\)
* valueOf\(\)

### false 복합 객체는 true로 변환된다

false 불리언 객체\(원시값과 대조되는 개념으로 사용\)는 Boolean\(\)  생성자와 new 키워드를 사용해 만들며, 객체는 true로 변환된다. 따라서 Boolean\(\)  생성자를 통해 만든 false 불리언 객체는 true로 변환된다. 

```javascript
var falseValue = new Boolean(false);
console.log(falseValue);    // false 불리언 객체지만, 객체는 true처럼 취급된다.

if (falseValue) {    // false 불리언 객체라 하더라도, 불리언 객체는 true처럼 취급된다.
    console.log('falseValue is truthy');
}
```

불리언 자료형이 아닌 값을 불리언값으로 변환하고 싶을 때는 new 키워드없이 Boolean\(\) 생성자만 사용하면 된다. 이 때 반환되는 결과값은 불리언 객체가 아닌 원시값이다.

### 일부 값은 false이고, 그 외는 true다

```javascript
// 여기서 사용한 값들은 모두 false 불리언값을 반환한다.
console.log(Boolean(0));
console.log(Boolean(-0));
console.log(Boolean(null));
console.log(Boolean(false));
console.log(Boolean(''));
console.log(Boolean(undefined));
console.log(Boolean(null));

// 여기서 사용한 값들은 모두 true 불리언값을 반환한다.
console.log(Boolean(1789));
console.log(Boolean('false'));    // 문자열 'false'는 false 불리언값으로 변환되지 않는다.
console.log(Boolean(Math));
console.log(Boolean(Array()));
```

**자바스크립트의 값 중 일부는 false로 자동 변환되고, 그 외의 다른 값은 true로 취급된다.**

