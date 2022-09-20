---
description: 제 6장
---

# this 키워드

### &#x20;this의 사용

함수를 만들 때는 함수를 실행하는 객체와 연결되는 this라는 키워드도 같이 만들어진다. 다시 말해, this는 함수의 스코프 안에서 사용할 수 있으며 함수를 속성 또는 메소드로 포함하고 있는 객체를 참조한다.

```javascript
var cody = {
    living: true,
    age: 23,
    gender: 'male',
    getGender: function() {
        return cody.gender;
    }
};

console.log(cody.getGender());    // 'male'이 기록된다.

var cody = {
    living: true,
    age: 23,
    gender: 'male',
    getGender: function() {
        return this.gender;
    }
};

console.log(cody.getGender());    // 'male'이 기록된다.
```

여기서 this.gender의 this는 현재 함수를 실행하고 있는 cody 객체를 참조한다. **함수 안에서 사용된 this는 일반적으로 함수 자체가 아닌 함수를 포하고 있는 객체를 참조한다고 생각하면 된다**(단, new 키워드, call(), apply()를 사용하는 경우는 예외)

### this의 값은 어떻게 정해지는(호출하는 방법에 따라서 달라짐)

```javascript
var foo = 'foo';
var myObject = {
    foo: 'I am myObject.foo'
};

var sayFoo = function() {
    console.log(this['foo']);    // this['foo']와 this.foo는 동일
}

// sayFoo 함수를 myObject의 sayFoo 속성으로 추가한다.
myObject.sayFoo = sayFoo;

myObject.sayFoo();    // 'I am myObject.foo'가 기록된다.
sayFoo();            //  'foo'가 기록된다.

// 이유는 myObject.sayFoo 입장에서 this 는 myObject 이기 떄문에 myObject.foo를 호출해 'I am myObject.foo'가 기록됨.
// sayFoo()는 this 가 window이기 때문에 window.sayFoo()를 호출. this.foo를 호출해 'foo'가 기록됨.
```

함수가 실행된 곳에 따라 this의 값이 달라지는 것을 볼 수 있음.

### 중첩된 함수 문제는 스코프 체인을 사용해 우회하라

스코프 체인을 사용해 부모 함수의 this에 대한 참조를 저장해두면 this값이 사라지는 것을 막을 수 있다. 다음 코드는 that 변수와 이 변수의 스코프를 사용해 함수 컨텍스트가 변하는 와중에도 this값을 유지하고 있다.

```javascript
var myObject = {
    myProperty: 'I can see the light',
    myMethod: funciton() {
        var that = this;
        var helperFunction = function() {
            console.log(that.myProperty);    // 'I can see the light'가 기록됨.
            console.log(this);               // window가 기록됨.
        }();
    }
};

myObject.myMethod();
```

### call() 또는 apply()를 사용한 this 값 설정(call() 또는 apply()를 통해 자바스크립트가 함수 스코프 내에 설정한 this의 값을 재정의할 수 있다.)

this의 값은 함수가 호출된 컨텍스트에 따라 보통 달라진다(new 키워드를 사용한 경우는 예외다.) 하지만 apply()나 call()을 사용해 함수를 호출할 때 this가 참조할 객체를 정해주는 식으로 this의 값을 조작할 수 있다. 이 방식을 사용하면 바로 자바스크립트에서 설정한 this의 값을 재정의할 수 있다.

다음 코드는 하나의 객체와 하나의 함수를 정의한 후 call()을 사용해 함수를 호출하며, 함수 내부의 this값으로 myObject를 사용하도록 했다. 이제 myFunction 함수 내부의 문장은 머리 객체가 아닌 myObject의 속성을 설정할 수 있게 된다. 이와 같이 this가 참조하는 값을 다른 객체로 대체할 수 있다.

```javascript
var myObject = {};

var myFunction = function(param1, param2) {
    // call()을 사용해 함수를 호출하며 this가 myObject를 가리키도록 설정한다.
    this.foo = param1;
    this.bar = param2;
    console.log(this);
}

myFunction.call(myObject, 'foo', 'bar');    // 함수를 호출하며 myObject를 this로 설정한다.

console.log(myObject);    // Object {foo = 'foo', bar = 'bar'}가 기록된다.

var myFunction2 = function(param1, param2) {
    // apply()를 사용해 함수를 호출하며 'this'가 myObject를 가리키도록 설정한다.
    this.foo = param1;
    this.bar = param2;
    console.log(this);
}

myFunction2.apply(myObject, ['foo', 'bar']);    // 함수를 호출하며 this를 설정한다.

console.log(myObject);    // Object {foo = 'foo', bar = 'bar'}가 기록된다.
```

**apply()와  call()의 차이점은 함수에 매개변수를 전달하는 방식뿐이다.** call()을 사용할 때는 쉼표로 값을 구분해 매개변수를 전달해야 하지만, apply()를 사용할 때는 뱅려 안에 값을 집어넣어 전달해야 한다.

### 사용자 정의 생성자 함수 내에서 this 키워드 사용하기

new 키워드를 사용해 함수를 실행할 때 생성자 함수 내에 코딩된 this의 값은 생성자의 인스턴스를 가리킨다. 다시 말해, 생성자 함수 내에서 우리는 실제로 객체가 만들어지기 전에도 this를 통해 인스턴스를 참조할 수 있다는 것이다. 이때 this의 기본값이 변경되는 방식은 call() 또는 apply()를 사용한 것과 크게 다르지 않다.

```javascript
var Person = function(name) {
    this.name = name || 'john doe';    // this는 만들어질 인스턴스를 참조한다.
}

var cody = new Person('Cody Lindley');    // Person 생성자를 사용해 인스턴스를 만든다.

console.log(cody.name);    // 'Cody Lindley'가 기록된다.
```

new 키워드를 사용해 생성자 함수를 호출하면 이때의 this는 "만들어질 객체"를 참조한다. 만약 우리가 new 키워드를 사용하지 않았다면 this의 값은 Person 함수가 호출된 컨텍스트(=window)가 되었을 것이다. 이 시나리오대로 동작하는지 아래 코드를 보자.

```javascript
var Person = function(name) {
    this.name = name || 'john doe';
}

var cody = Person('Cody Lindley');    // 여기서는 new를 사용하지 않음.

// cody는 undefined이다. name 값은 실제로는 window.name에 설정되어 있다.
console.log(cody.name);

console.log(window.name);    // 'Cody Lindley'가 기록된다.
```

### 프로타입 메소드 안의 this는 생성자 인스턴스를 참조한다

생성자의 prototype 속성에 추가한 함수를 사용할 때 this는 메소드를 실행한 인스턴스를 참조한다.&#x20;

```javascript
var Person = function(x) {
    if (x) {
        this.fullName = x;
    }
}

Person.prototype.whatIsMyFullname = function() {
    return this.fullName;    // this 는 Person() 을 통해 만들어진 인스턴스를 참조한다.
}

var cody = new Person('cody lindley');
var lisa = new Person('lisa lindley');

// 상속한 whatIsMyFullname 메소드를 호출한다. 이 메소드 안의 this는 해당 인스턴스를 참조할 것이다.
// 생성자함수: Person, 인스턴스: cody, lisa(생성자 함수를 이용해 만들어진 객체를 인스턴스라고 한다.)
console.log(cody.whatIsMyFullname(), lisa.whatIsMyFullname());

// 프로토타입 체인도 여전히 적용된다. 따라서 인스턴스가 fullName 속성을 포함하고 있지 않으면 프로토타입 체인에서 이 속성을 갖는다.
// 다음에서 우리는 fullName 속성을 Person prototype과 Object.prototype 양쪽에 추가했다.

Object.prototype.fullName = 'John Doe';
var john = new Person();    // 전달된 인수가 없으므로 인스턴스에는 fullName 속성이 설정되지 않는다.

console.log(john.whatIsMyFullname());    // 'John Doe' 가 기록된다.

```

this 키워드는 prototype 객체에 포함된 메소드 내에서 인스턴스를 참조할 때 사용한다. 찾는 속성이 인스턴스에 없으면 프로토타입 체인을 검색한다.
