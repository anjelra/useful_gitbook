---
description: 제 3장
---

# Object()

### Object()  객체 사용

```javascript
var cody = new Object();    // 속성이 없는 빈 객체를 만듦.

for (key in cody) {    // cody가 범용 빈 객체인지 확인함.
    if (cody.hasOwnProperty(key)) {
        console.log(key);    // cody 자체에는 속성이 없기 때문에 아무런 로그도 보이지 않아야 함.
    }
}
```

* 내장 Object() 생성자 함수를 사용하면 범용 빈 객체를 바로 만들 수 있음.
* Object() 생성자는 그 자체도 객체. 'Array 생성자처럼 Object 생성자도 빈 객체를 만들어 낸다고 생각하면 이해하기가 쉬움'\


### Object()의 속성과 메소드

#### 속성(예: Object.prototype)

* prototype (최상위 객체)

### Object() 객체 인스턴스의 속성과 메소드

#### 인스턴스 속성(예: var myObject = {}; myObject.constructor;)

* constructor

#### 인스턴스 메소드(예: var myObject = {}; myObject.toString();)

* hasOwnProperty()
* isPrototypeOf()
* propertyIsEnumerable()
* toLocaleString()
* toString()
* valueOf()

### "객체 리터럴"을 사용한 Object() 객체 생성

```javascript
var cody = new Object();
cody.living = true;
cody.age = 33;
cody.gender = 'male';
cody.getGender = function() {return cody.gender;};

console.log(cody);    // cody 객체와 속성을 기록함.
```

#### 객체 리터럴을 이용하면?? 훨씬 간결해지고 시간도 적게 걸림.

```javascript
var cody = {
    living: true,
    age: 23,
    gender: 'male',
    getGender: function() {return cody.gender;}
};

console.log(cody);    // cody 객체와 속성을 기록함.
```

### 모든 객체는 Object.prototype을 상속받는다.

* object() 생성자 함수의 prototype 속성은 프로토타입 체인의 가장 끝에 있음. 아래의 코드를 보자.

```javascript
Object.prototype.foo = 'foo';

var myString = 'bar';

// 'foo'가 기록. 이 값은 프로토타입 체인을 통해 Object.prototype.foo에서 가져옴.
console.log(myString.foo);
```

* 위의 코드에서 보면 Object.prototype에 foo 속성을 추가한 후 문자열을 하나 만들고 문자열 인스턴스의 foo 속성에 접근했음. myString 인스턴스에는 foo 속성이 없으므로 프로토타입 체인의 효과가 나타나 String.prototype에서 foo 속성을 찾음. 여기에도 없으므로 그 다음으로는 Object.prototype에서 찾음. object.prototype은 자바스크립트가 객체의 속성을 찾을 때 마지막으로 확인하는 곳임. Object.prototype에 foo라는 값을 추가했으므로 Object.prototyp에는 foo 속성이 있을 테고 이 속성은 "foo"를 반환함.
