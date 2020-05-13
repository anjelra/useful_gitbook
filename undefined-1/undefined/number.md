---
description: 제 11장
---

# Number\(\)

### Number\(\) 객체의 사용

 Number\(\) 생성자 함수는 숫자 객체와 숫자 원시값을 만들 때 사용한다.

```javascript
// new 키워드와 Number() 생성자를 사용해 숫자 객체를 만든다.
var numberObject = new Number(1);
console.log(numberObject);    // 1이 기록된다.
console.log(typeof numberObject);    // 'object'가 기록된다.

// new 키워드 없이 생성자만 사용해 리터럴/원시 숫자값을 만든다.
var numberObjectWithOutNew = Number(1);
console.log(numberObjectWithOutNew);    // 1이 기록된다.
console.log(typeof numberObjectWithOutNew);    // 'number'가 기록된다.

var numberLiteral = 1;
console.log(numberLiteral);    // 1이 기록된다.
console.log(typeof numberLiteral);    // 'number'가 기록된다.
```

### 정수와 실수

```javascript
var integer = 1231234;
console.log(integer);    // '1231234'가 기록된다.

var floatingPoint = 2.132;
console.log(floatingPoint);    // '2.132'가 기록된다.
```

### Number\(\) 매개변수

```javascript
var numberOne = new Number(456);

console.log(numberOne);    // '456{}'가 기록된다.
```

**Number\(\) 생성자와 new 키워드를 사용해 만든 인스턴스는 실제로는 복합 객체를 만들어낸다. 따라서 typeof  연산자와 관련한 문제가 발생할 수 있으므로 가능하다면 숫자값을 만들 때는 Number\(\)  생성자를 명시적으로 사용하지 않는 것이 좋다\(대신 리터럴/원시값을 권장한다\). typeof 연산자를 사용하면 원시값에 대해서는 'number'라고 기대했던 대로 알려주지만 숫자 객체에 대해서는 'object\(객체\)'라고 알려준다. 게다가 리터럴/원시값이 더 간결하다.**

### Number\(\) 속성

#### 속성

* MAX\_VALUE
* MIN\_VALUE
* NaN
* NEGATIVE\_INFINITY
* POSITIVE\_INFINITY
* prototype

### Number 객체 인스턴스의 속성과 메소드

#### 인스턴스 속성

* constructor

#### 인스턴스 메소드

* toExponential\(\) -&gt; 숫자를 지수 표기법으로 표기해 반환.
* toFixed\(\) -&gt; 숫자를 고정 소수점 표기법으로 표기해 반환.
* toLocaleString\(\) -&gt; 숫자의 언어 구분이 포함된 문자열을 반환.
* toPrecision\(\) -&gt; 지정된 정밀도로 나타내는 문자열을 반환.
* toString\(\)
* valueOf\(\)

