---
description: 제 6장
---

# this 키워드

###  this의 사용

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

여기서 this.gender의 this는 현재 함수를 실행하고 있는 cody 객체를 참조한다. **함수 안에서 사용된 this는 일반적으로 함수 자체가 아닌 함수를 포하고 있는 객체를 참조한다고 생각하면 된다**\(단, new 키워드, call\(\), apply\(\)를 사용하는 경우는 예외\)

### this의 값은 어떻게 정해지는\(호출하는 방법에 따라서 달라짐\)

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





