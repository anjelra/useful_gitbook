---
description: 제 10장
---

# String()

### String() 객체의 사용

String()  생성자 함수는 문자열 객체와 문자열 원시값을 만들 때 사용한다.

```javascript
// new 키워드와 String() 생성자를 사용해 문자열 객체를 만든다.
var stringObject = new String('foo');
console.log(stringObject);    // foo {0 = 'f', 1 = 'o', 2 = 'o'}
console.log(typeof stringObject);    // 'object'가 기록된다.

// new 키워드 없이 생성자만 사용해 리터럴/원시 문자열을 만든다.
var stringObjectWithOutNewKeyword = String('foo');
console.log(stringObjectWithOutNewKeyword);    // 'foo'가 기록된다.
console.log(typeof stringObjectWithOutNewKeyword);    // 'string'이 기록된다.

// 리터럴/원시 문자열을 만든다(생성자가 암묵적으로 사용됨).
var stringLiteral = 'foo';
console.log(stringLiteral);    // 'foo'가 기록된다.
console.log(ytpeof stringLiteral);    // 'string'이 기록된다.

// new 키워드와 생성자를 사용하는 것과 string 문자를 사용하는 것은 엄연히 다르다. 눈에는 같아 보이지만
var myString = new String('male');    // 객체
var myStringLiteral = 'male';            // 원시 문자열값. 객체가 아님!!!!!
```

### String() 매개변수

String() 생성자에는 만들 객체가 가질 문자열값을 매개변수로 전달할 수 있다.

```javascript
// 문자열 객체를 만든다.
var stringObject = new String('foo');

console.log(stringObject);    // 'foo {0="f", 1="o", 2="o"}가 기록된다.'
```

**String() 생성자와 new 키워드를 사용해 만든 인스턴스는 실제로는 복합 객체를 만들어낸다. 따라서 typeof 연산자와 관련한 문제가 발생할 수 있으므로 가능하다면 문자열을 만들 때는 String() 생성자를 명시적으로 사용하지 않는 것이 좋다(대신 리터럴/원시값을 권장한다.).  typeof 연산자를 사용하면 원시값에 대해서는 'string'이라고 기대했던 대로 알려주지만 문자열 객체에 대해서는 'object(객체)'라고 알려준다. 게다가 리터럴/원시값을 작성하는 편이 더 빠르고 간편하다.**

### **String()  속성과 메소드(상속받은 속성과 메소드 제외)**

#### **속성**

* Prototype

#### 메소드

* fromCharCode()

### String 객체 인스턴스의 속성과 메소드

#### 인스턴스 속성

* constructor
* length

#### &#x20;인스턴스 메소드

* charAt()
* charCodeAt()
* concat()
* indexOf()
* lastIndexOf()
* localeCompare()
* match()
* quote()
* replace()
* search()
* slice()
* split()
* substr()
* substring()
* toLocaleLowerCase()
* toLocaleUpperCase()
* toLowerCase()
* toString()
* toUpperCase()
* valueOf()



****
