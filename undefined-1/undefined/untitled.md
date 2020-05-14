---
description: 제 1장
---

# 자바스크립트 객체

### 객체 만들기 

* 자바스크립트에서는 객체가 왕. 거의 모든 것들이 객체이거나 객체처럼 동작함.
* 객체는 이름이 있는 값들\(속성\)의 집합.
* 프로그래밍을 추가하지 않는다면 우리가 다루고 있는 JSON 과 유사할 뿐임.

```javascript
// cody 객체 만들기
var cody = new Object();

// cody 객체를 속성으로 채우기 (점 표기법 사용)
cody.living = true;
cody.age = 33;
cody.gender = 'male';

console.log(cody);    // 객체를 로그에 출력 {living = true, age = 33, gedner = 'male'}
```

### 생명력 부여\(메소드 추가\)

```javascript
// cody 객체 만들기
var cody = new Object();

// cody 객체를 속성으로 채우기 (점 표기법 사용)
cody.living = true;
cody.age = 33;
cody.gender = 'male';
cody.getGender = function() {return cody.gender;};
console.log(cody.getGender());    // 'male'이 출력된다.
```

### string\(\), object\(\) 생성자 함수를 이용하면 객체로 표현할 수 있음.

```javascript
var myObject = new Object();    // Object() 객체 만들기
myObject['0'] = 'f';
myObject['1'] = 'o';
myObject['2'] = 'o';

console.log(myObject);    // Object {0="f", 1="o", 2="o"}가 기록됨.

var myString = new String('foo');    // String() 객체 만들기
console.log(myString);    // foo {0="f", 1="o", 2="o"}가 기록됨.

// 보통 문자열은 원시값으로 사용되기 때문에 (ex: var myString = 'foo';) 객체 형태로 보이는게 
// 이상할 수 있지만 자바스크립트는 무엇이든 객체가 될 수 있다. 
```

### 사용자 정의 객체로생성자 함수를 만들 수 있음.

```javascript
// Person() 객체를 만들기 위해 Person 생성자 함수를 정의함.
var Person = function(living, age, gender) {
    this.living = living;
    this.age = age;
    this.gender = gender;
    this.getGender = function() {return this.gender;};
}

// Person 객체의 인스턴스를 만들고 cody라는 변수를 저장함.
var cody = new Person(true, 33, 'male');

console.log(cody);
```

### 자바스크립트 생성자는 객체 인스턴스를 생성하고 반환한다.

new 키워드를 사용하면 자바스크립트가 생성자 함수 내에 있는 this의 값을 새로 만들어진 객체로 설정함으로써 생성자 함수는 특수한 동작을 수행하게 된다. 특수한 동작을 한 생성자 함수는 기본값인 거짓스러운 값\(null, undefined, 0, 빈 문자열과 같이 false는 아니지만 마치 false처럼 사용할 수 있는 값을 가리킴\)이 아닌 새로 만든 객체\(즉, this\)를 반환한다. 생성자 함수가 반환한 새 객체는 객체를 만든 생성자 함수의 인스턴스\(instance\)라 부른다.

#### Person은 생성자 함수, cody는 인스턴스. 

```javascript
// Person은 생성자 함수이며, new 키워드와 함께 사용하도록 만들어짐.
var Person = function Person(living, age, gender) {
    // 아래에서 'this'는 새롭게 작성된 객체(this = new Object();)를 뜻함.
    this.living = living;
    this.age = age;
    this.gender = gender;
    this.getGender = function() {return this.gender;};
    // new 키워드와 함께 생성자 함수를 호출하면 undefined 대신 'this'가 반환됨.
}

// Person 객체의 인스턴스를 만들어 cody에 저장한다.
var cody = new Person(true, 33, 'male');

// cody는 Person()의 객체이자 인스턴스다.
console.log(typeof cody);         // object가 기록된다.
console.log(cody);                // cody가 포함한 속성과 같은 값이 기록된다.
console.log(cody.constructor);    // Person() 함수가 기록된다.
```

```javascript
// Array 객체의 인스턴스를 만들어 myArray에 저장한다.
var myArray = new Array();    // myArray는 Array의 인스턴스다.

// myArray는 Array() 생성자의 객체이자 인스턴스다.
console.log(typeof myArray);    // object가 기록된다. 배열은 객체(object)의 한 종류다.

console.log(myArray);    // []가 기록된다.

console.log(myArray.constructor);    // Array()가 기록된다.
```

### 자바스크립트 네이티브/ 내장 객체 생성자 \(new를 사용해서 객체 생성\)

* Number\(\)
* String\(\)
* Boolean\(\)
* Object\(\)
* Array\(\)
* Function\(\)
* Date\(\)
* RegExp\(\)
* Error\(\)

### 사용자 정의 객체 생성자 함수

```javascript
var Person = function Person(living, age, gender) {
    this.living = living;
    this.age = age;
    this.gender = gender;
    this.getGender = function() {return this.gender;};
}

var cody = new Person(true, 33, 'male');
console.log(cody);

var lisa = new Person(true, 34, 'female');
console.log(lisa);
```

* 사용자 정의 객체의 장점은 속성의 값은 다르게 사용하는 객체를 둘 또는 셋 이상 만들어야 하는 경우에 매우 편리함.
* 생성자 함수의 첫 문자는 대문자로 하는 것이 좋음.

### new 연산자를 사용한 생성자 인스턴스 생성

9개의 미리 정의된 네이티브 생성자 함수와 new 연산자를 함께 사용하면 객체의 인스턴스를 얻을 수 있음.

```javascript
// new 키워드를 사용한 각 네이티브 생성자의 인스턴스 생성
var myNumber = new Number(23);
var myString = new String('male');
var myBoolean = new Boolean(false);
var myObject = new Object();
var myArray = new Array('foo', 'bar');
var myFunction = new Function("x", "y", "return x*y");
var myDate = new Date();
var myRegExp = new RegExp('\bt[a-z]+b');
var myError = new Error('Crap!');

// 만들어진 객체의 생성자가 무엇인지 기록 및 확인
console.log(myNumber.constructor);    // Number()가 기록됨.
...
console.log(myArray.constructor);    // 최신 브라우저에서는 Array()가 기록됨.
...
```

### 리터럴을 사용한 값 생성하기

* 자바스크립트에는 new Foo\(\) 또는 new Bar\(\) 같은 방법을 사용하지 않아도 대부분의 제이티브 객체값을 만들 수 있는 "리터널\(literal\)"이라는 축약 표현이 있음.
* Number\(\), String\(\), Boolean\(\) 을 제외한 대부분의 경우 리터럴 문법은 new 연산자를 사용할 때와 같다.

```javascript
var myNumber = new Number(23);    // 객체
var myNumberLiteral = 23;         // 원시 숫자값. 객체가 아님

var myString = new String('male');    // 객체
var myStringLiteral = 'male';         // 원시 문자열값. 객체가 아님

var myBoolean = new Boolean(false);    // 객체
var myBooleanLiteral = false;          // 원시 불리언값. 객체가 아님

var myObject = new Object();
var myObjectLiteral = {};

var myArray = new Array('foo', 'bar');
var myArrayLiteral = ['foo', 'bar'];

var myFunction = new Function("x", "y", "return x*y");
var myFunctionLiteral = function(x, y) {return x*y};

var myRegExp = new RegExp('\bt[a-z]+b');
var myRegExpLiteral = /\bt[a-z]+b/;
```

#### 리터널값의 메소드/속성에 접근하면 자바스크립트는 먼저 리터럴값에 해당하는 래퍼\(wrapper\) 객체를 만들고 이를 통해 메소드나 속성에 접근. 메소드를 호출하고 나면 래퍼 객체를 제거한 후 다시 값을 리터럴형으로 되돌림. 

#### 이 덕분에 문자열, 숫자, 불리언값은 원시\(혹은 단순\) 자료형으로 취급됨. 이런 특성이 있다는 것을 이해하여 "자바스크립트에서 모든 것은 객체처럼 동작한다"는 사실을 "자바스크립트에서 모든 것은 객체다"라는 말과 혼동하면 안됨.



### 원시값\(=단순값\)

true, false, null, undefined와 같은 자바스크립트값은 더 이상 단순화할 수 없기 때문에 원시적\(primitive\)라 하며, 이러한 값을 가리켜 원시값이라 한다. 즉, 숫자는 숫자이고 문자열은 문자열이며 불리언은 true 또는 false일테고, null 과 undefined는 단순히 null과 undefined라는 듯이다. 이러한 값은 본진적으로 단순하며, 다른 여러 값으로 구성된 값을 표현할 수 없다. 

### 원시값 null, undefined, "string", 10, true, false는 객체가 아니다!!

### 원시값은 어떻게 저장,복사되는가

```javascript
var myString = 'foo';    // 원시 문자열 객체를 만든다.
var myStringCopy = myString;    // 값을 새 변수로 복사한다.

var myString = null;    // myString 변수에 저장된 값을 수정한다.

console.log(myString, myStringCopy);    // 'null foo'가 기록된다.
```

원시값에 저장되고 수정되는 값은 더 이상 축약할 수 없는 값이며, 원시값을 참조하면 값 자체를 복사함. 위의 예제에서 myString값을 변수 myStringCopy에 복사 또는 복제함. myString의 값을 갱신해도 myStringCopy의 값은 여전히 myString에서 복사할 때의 값을 유지함. 이러나 특성은 복합 객체와 대조됨. 

### 원시값은 값 자체를 비교한다

```javascript
var price1 = 10;
var price2 = 10;
var price3 = new Number('10');    // new 키워드를 사용했으므로 price3은 복합 객체.
var price4 = price3;

console.log(price1 === price2);    // true

// price3은 복합 숫자 객체를 포함하고 있으나 price1은 원시값이므로 false
console.log(price1 === price3);

// 복합 객체는 값이 아닌 참조를 비교하므로 true가 기로됨.
console.log(price4 === price3);

// 원시값을 포함한 price4 변수의 값을 수정하면?
price4 = 10;

console.log(price4 === price3);    // false(지금 price4는 복합 객체가 아닌 원시값이기 떄문에)
```

원시값은 비교할 때 값 자체가 같은지 비교함. new 키워드를 사용해 만든 문자열, 숫자, 불리언 값을\(ex: new Number\('10'\)\) 비교할 때는 원시값으로 취급하지 않음. 따라서 리터럴 문법을 사용해 만든 값과 new 키워드를 사용해 만든 값을 비교하면 항상 같지 않다고 나타남. 원시값은 저장된 값을 비교하는 반면, 복합 객체는 저장된 참조를 비교하기 때문임.

### 복합 객체\(=합성 객체\)

* Object\(\), Array\(0, Function\(\), Date\(\), Error\(\), RegExp\(\)  와 같은 네이티브 객체 생성자들은 한 개 이상의 원시값이나 복합 객체를 저장할 수 있기 때문에 복합적이라 볼 수 있음.
* 복합 객체는 여러 값을 하나로 합친 합성체이며, 여러 값을 복합적으로 구성할 수 있다는 점에서 원시값과 구별됨.
* 복합 객체 = 합성 객체 = 참조 객체 = 참조 자료형

### 복합 객체는 어떻게 저장, 복사되는가

* 복합 객체가 참조\(reference\)에 의해 저장되고 조작된다는 것은 반드시 이해하고 가야할 중요한 사실.
* 복합 객체를 포함한 변수를 만들면 이 값은 메모리의 특정 주소에 저장되고, 복합 객체를 참조할 때 복합 객체의 이름\(즉, 변수나 객체 속성\)을 통해 메모리의 특정 주소에 있는 이 값에 접근함. 이런 특성은 복합값을 복사하려고 할 때 매우 중요함.

```javascript
var myObject = {};

var copyOfMyObject = myObject;    // 값이 아닌 참조만 복사함.
myObject.foo = 'bar';    // myObject에 저장된 값을 수정함.

// 이제 myObject와 copyOfMyObject를 출력해보면 두 변수 모두 foo 속성을 가지고 있다는 것을 알 수 있음. 이는 두 변수가 같은 객체르 참조했기 때문임.
console.log(myObject, copyOfMyObject);    // Object{foo="bar"}, Object{foo="bar"}가 기록됨.
```

* 중요한 사실은 값 자체가 복사되던 원시값과는 달리 객체\(=복합 객체\)는 참조로 저장된다는 것임. 따라서, 참조\(=메모리 주소\)만 복사되고 실제 값은 복사되지 않음. 이는 곧 객체를 복사할 수 없다는 뜻이 됨. 복사되는 것은 메모리 저장공간에 있는 객체의 주소 또는 참조일 뿐임. myObject와 copyOfMyObject는 메모리에 있는 같은 객체를 가리키고 있음.  따라서 둘 중 한 변수의 값만 바꾸어도 두 변수의 값이 모두 변함.
* String\(\), Number\(\), Boolean\(\) 값은 new 키워드를 사용해 만들었거나 복합객체로 변환하더라도 값이 그대로 저장,복사 된다. 따라서 원시값을 복합 객체처럼 다룰 수 있는 경우에도 참조가 복사되지는 않는다.

### 복합 객체는 참조를 비교한다

```javascript
var objectFoo = {same: 'same'};
var objectBar = {same: 'same'};

// false가 기록. 자바스크립트에 두 객체가 동등한지 같은 자료형인지는 중요하지 않음.
console.log(objectFoo === objectBar);

// 두 복합 객체가 같은지 확인한다.
var objectA = {foo: 'bar'};
var objectB = objectA;

console.log(objectA === objectB);    // 두 변수가 모두 같은 객체를 참조하고 있으므로 true가 기록됨.
```

* 복합 객체를 가리키는 변수들은 변수가 메모리에서 모두 하나의 "주소"를 가리키고 있을 때만 서로 같다고 판단함. 이와 반대로, 두 개의 독립적인 객체는 자료형이나 속성이 똑같더라도 서로 다르다고 판단함.

### 복합 객체는 동적 속성을 포함한다 

```javascript
var objA = {property: 'value'};
var pointer1 = objA;
var pointer2 = pointer1;

// objA.property를 갱신하면, 참고(pointer1 과 pointer2)도 모두 갱신됨.
objA.property = null;

// objA, pointer1, pointer2는 모두 같은 객체를 가리키므로 'null, null, null'이 기록됨.
console.log(objA.property, pointer1.property, pointer2.property);
```

* 객체를 정의하고 참조를 만든 후 객체를 갱신하면 해당 객체를 가리키는 모든 참조도 같이 갱신되므로  동적인 객체 속성도 가능해짐.  

### 생성자 인스턴스에는 자신의 생성자 함수를 가리키는 속성이 있다

```javascript
var foo = {};

// Object()가 foo를 만들었으므로 true가 기록됨.
console.log(foo.constructor === Object);

// Object()를 가리
console.log(foo.constructor);
```

```javascript
var myNumber = new Number('23');
var myNumberL = 23;    // 리터럴 축약형

// true(myNumberL은 리터럴 축약형으로 만든 원시값이므로 myNumber === myNumberL은 false 이지만
// 생성자는 Number()로 같음.
console.log(myNumber.constructor === Number);
```

### 생성자를 통해 만든 인스턴스에 인스턴스 속성 추가하기

```javascript
var myString = new String();
var myNumber = new Number();

myString.prop = 'test';
myNumber.prop = 'test';

// 'test', 'test'가 기록
console.log(myString.prop, myNumber.prop);

// 주의!!!!!!!
// 원시값/리터럴 값에는 인스턴스 속성을 설정할 수 없다.
var myString = 'string';
var myNumber = 1;

myString.prop = true;
myNumber.prop = true;

// undefined, undefined가 기록됨.
console.log(myString.prop, myNumber.prop);
```

### 자바스크립트 객체와 Object\(\) 객체의 의미

* 자바스크립트 객체 : 모든 것을 객체라는 것을 의미
* Object\(\) 객체 : 생성자 역할의 객체를 의미 

