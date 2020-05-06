---
description: 제 8장
---

# 함수의 프로토타입

### 프로토타입 체인

자바스크립트는 Function\(\) 인스턴스에 자동으로 prototype이라는 속성을 만든다. 구체적으로 말하자면 prototype 속성은 new 키워드와 생성자 함수를 같이 사용해서 만든 객체에 연결된다. 인스턴스들은 생성자 함수의 prototype 속성을 통해 공통의 메소드와 속성을 공유하고 상속한다. 

```javascript
var myArray = new Array('foo', 'bar');
console.log(myArray.join());    // 'foo', 'bar'가 출력된다.
```

### prototype 속성이 왜 중요한가

1. 네이티브 생성자 함수\(예:Object\(\), Array\(\), Function\(\) 등\)는 prototype 속성을 사용해 생성자 인스턴스가 메소드와 속성을 상속받도록 하고 있기 때문이다. 자바스크립트는 이러한 메커니즘을 사용해 객체 인스턴스가 생성자 함수의 prototype 속성을 상속받을 수 있도록 지원해 준다. 따라서 자바스크립트를 더 잘 이해하려면 자바스크립트가 prototype 객체를 어떻게 사용하는지 잘 알아야 한다.
2. 사용자 정의 생성자 함수를 만들 때 자바스크립트 네이티브 객체와 동일한 방식을 통해 프로토타입 상속을 구현할 수 있기 때문이다. 그러나 상속이 이루어지는 방식에 대한 이해가 반드시 수반되어야 한다.
3. 프로토타입 상속을 정말 싫어하거나 다른 상속 패턴을 더 좋아할 수도 있지만 현실적으로 생각해 볼 때 아마도 누군가 프로토타입 상속을 용해 구현해놓은 코드를 수정하거나 조작해야 할 일이 있을 것이다. 이때 프로토타입 상속이 어떻게 동작하는지 알아야 다른 개발자가 만든 생성자 함수의 기능을 그대로 복제할 수 있을 것이다.
4. 프로토타입 상속을 사용하면 동일한 메소드를 공유하는 여러 개의 효율적인 객체 인스턴스를 만들 수 있다. 앞서 말한 것과 같이 Array\(\) 생성자의 인스턴스인 배열 객체는 굳이 인스턴스마다 join\(\) 메소드를 추가해주지 않아도 된다. 모든 배열 인스턴스의 프로토타입 체인에는 join\(\) 메소드가 저장되어 있으므로 모든 배열 인스턴스는 동일한 join\(\) 메소드를 사용할 수 있다.

### 모든 Function\(\) 인스턴스는 prototype 속성이 있다

자바스크립트에서 함수는 Function\(\) 생성자를 직접 호출하여 만들었든\(ex: var add = new Function\('x', 'y', 'return x + y'\);\); 리터럴 표기법을 사용해 만들었든\(ex: var add = function\(x, y\) { return x + y };\) 예외 없이 모두 Function\(\) 생성자로부터 만들어진다.

함수 인스턴스를 만들면 인스턴스에는 항상 prototype 속성이 추가된다. 이때, prototype 속성은 그 자체로는 빈 객체와 같다. 다음 코드에서 우리는 myFunction이라는 함수를 정의한 후, 이 함수의 prototype 속성에 접근했다.

```javascript
var myFunction = function() {};
console.log(myFunction.prototype);    // Object{}가 기록된다.
console.log(typeof myFunction.prototype);    // 'object'가 기록된다.
```

**Funciton\(\) 생성자를 사용할 때면 언제나 자동으로 설정되는 prototype 속성**은 중요한 속성이니만큼 완벽히 이해해야 한다. 

### prototype 속성은 Object\(\) 객체다

엄밀히 말해 prototype은 Function\(\) 인스턴스를 만들 때 자바스크립트가 인스턴스에 부여하는, 이름이 "prototype"이고 기본값이 빈 객체인 속성일 뿐이다. 만약 이를 사용자가 직접 코드로 만든다면 다음과 같이 작성할 수 있을 것이다.

```javascript
var myFunction = function() {};

myFunction.prototype = {};    // prototype 속성을 추가하고 속성값으로 빈 객체를 할당한다.
console.log(myFunction.prototype);    // 빈 객체가 기록된다.
```

### 생성자 함수를 통해 만든 인스턴스는 생성자 함수의 prototype 속성과 연결되어 있다

생성자 함수의 prototype 속성은 그 자체만 놓고보면 객체일 뿐이지만 프로토타입 체인을 통해 인스턴스와 연결되는 특이한 속성이다. 다시 말해, new 키워드와 생성자 함수를 사용해 객체를 만들면 생성자 함수의 prototype 속성과 새롭게 만들어진 객체 인스턴스 사이에는 일종의 숨겨진 연결고리가 생긴다. 일부 브라우저에서는 이 연결고리가 인스턴스의 \_\_proto\_\_ 속성으로 나타나기도 한다. 자바스크립트는 생성자 함수를 사용해 인스턴스를 만들 때 인스턴스 객체와 생성자 함수를 자동으로 연결해두며, 이러한 연결 덕분에 프로토타입 체인이 형성된다.

```javascript
// 이 코드는 __proto__를 사용할 수 있는 브라우저에서만 동작한다.
Array.prototype.foo = 'foo';
var myArray = new Array();

console.log(myArray.__proto__.foo);    // myArray.__proto__ = Array.prototype 이므로 foo가 기록된다.
```



