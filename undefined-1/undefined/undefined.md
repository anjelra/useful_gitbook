---
description: 제 2장
---

# 객체와 속성 다루기

### 복합 객체는 자바스크립트 자료형의 대부분을 속성으로 포함할 수 있다

```javascript
var myObject = {};

// 네이티브 자바스크립트의 자료형 대부분을 myObject의 내부에 속성으로 포함한다.
myObject.myFunction = function() {};
myObject.myArray = [];
myObject.myString = 'string';
myObject.myNumber = 33;
myObject.myDate = new Date();
myObject.myRegExp = /a/;
myObject.myNull = null;
myObject.myUndefined = undefined;
myObject.myObject = {};
myObject.myMath_PI = Math.PI;
myObject.myError = new Error('Crap!');

// 다른 복합 객체(예: 함수)도 이와 똑같이 작동한다.
var myFunction = function() {};

myFunction.myFunction = function() {};
myFunction.myArray = [];
...
```

### 복합 객체에 대른 객체 포함하기

```javascript
// 객체를 사용한 캡슐화, 객체 체인을 만듦.
var object1 = {
    object1_1: {
        object1_1_1: {foo: 'bar'},
        object1_1_2: {}
    },
     object1_2: {
        object1_2_1: {},
        object1_2_2: {}
    }
};

// 'bar'가 기록됨.
console.log(object1.object1_1.object1_1_1.foo);
```

* Array\(\), Function\(\) 객체와도 가능함.\(이를 다중 배열이라고 부름\) 

### 점 표기법과 각괄호 표기법을 사용한 객체 속성 접근

* 점 표기

```javascript
var copdy = new Object();

cody.living = true;
cody.age = 33;
cody.gender = 'male';
cody.getGender = function() {return cody.gender};

// true를 가져
console.log(cody.living);

// 속성을 갱신
cody.living = false;
cody.age = 99;
cody.gender = 'female';
cody.getGender = function() {return 'Gender = ' + cody.gender};
```

* 각괄호 표기법

```javascript
var copdy = new Object();

cody['living'] = true;
cody['age'] = 'male';
...

console.log(cody['living']);

// 속성을 갱신
cody['living'] = false;
cody['age'] = 99;
...
```

#### 일반적으로는 점 표기법을 많이 쓰긴 하나, 각괄호 표기법이 유용한 경우가 있음. 아래의 예제를 보자.

```javascript
var foobarObject = {foobar: '"foobar"는 의미 없는 코드를 표현할 때 사용합니다.'};

var string1 = 'foo';
var string2 = 'bar';

console.log(foobarObject[string1 + string2]);
```

* 각괄호 표기법을 사용하면 자바스크립트 식별자로 사용할 수 없는 속성 이름도 사용할 수 있음.
* 숫자와 예약어를 속성 이름으로 사용할 경우 각괄호 표기법을 통해서만 접근할 수 있음.

```javascript
//점 표기법으로는 불가능. 자바스크립트에서 'class'는 예약어이기 때문에. 그러나 각괄호 표기법에서는 가능함.
console.log(myObject['123'], myObject['class']);
```

### 객체 속성 삭제하기 

```javascript
var foo = {bar: 'bar'};
delete foo.bar;
console.log('bar' in foo);    // bar는 foo에서 제거했기 때문에 false가 기록됨.
```

### 객체 속성의 참조를 찾는 법

* 접근한 속성이 객체에 포함되어 있지 않으면 자바스크립트는 항상 프로토타입 체인을 이용해 속성과 메소드를 찾음.
* 모든 객체 인스턴스는 인스턴스를 만든 생성자 함수를 가리키는 비밀 링크\(이를 \_\_proto\_\_라 부른다\)를 속성으로 가지고 있음.

```javascript
var myArray = ['foo', 'bar'];

console.log(myArray.join());
```

```javascript
var myArray = ['foo', 'bar'];

console.log(myArray.hasOwnProperty('join');    // false가 기록됨.
```

* join\(\) 메소드는 myArray 객체 안에서 정의되지 않았음. 그런데 사용을 할 수 있는 이유는 프로토타입 체인 규칙이 적용되어 자바스크립트는 Array 생성자의 prototype 속성\(Array.prototype\)에서 join\(\) 메소드를 찾음. 하지만 여기에서는 볼 수 없으므로 다시 프로토타입 체인 규칙이 적용되어 Object\(\)의 prototype 속성\(Object.prototype\)에서 이 메소드를 찾음. 만약 여기에서도 찾지 못했다면 자바스크립트는 메소드가 정의되지 않았다며 undefined 에러를 발생시켰을 것. 
* prototype 속성은 모두 객체이며 프로토타입 체인의 종점은 Object.prototype임. 그 뒤로 조사해 볼 수 있는 prototype 속성은 없음.

### hasOwnProperty를 사용해 프로토타입 체인에서 상속받은 속성인지 확인하기

```javascript
var myObject = {foo: 'value'};

console.log(myObject.hasOwnProperty('foo'));    // true 가 기록.

// 프로토타입 체인에서 상속받은 속성과 비교
console.log(myObject.hasOwnProperty('toString'));    // false가 기록.
```

* hasOwnProperty 메소드를 사용하면 객체의 속성이 프로토타입 체인에서 상속받지 않은 해당 객체의 고유한 것인지를 확인할 수 있음.
* 객체 자체의 속성인지 혹은 프로토타입 체인에서 상속받은 속성인지 확인하려면 반드시 hasOwnProperty 메소드의 도움을 받아야 함.

### in 연산자를 사용해 객체가 주어진 속성을 포함하는지 확인하기

* in연산자는 참조한 객체에 포함된 속성은 물론 해당 객체가 프로토타입 체인을 통해 상속받은 속성도 확인함.

```javascript
var myObject = {foo: 'value'};
console.log('toString' in myObject);    // true가 기록됨.
```

* toString 속성은 myObject 객체의 내부에는 없는 속성임. 하지만 Object.prototype에서 상속받은 속성이므로 in 연산자는 myObject가 실제로는 상속받은 toString\(\) 속성 메소드를 가지고 있다고 판단함.

