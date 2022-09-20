---
description: 제 4장
---

# Function\(\)

### Function\(\) 객체 사용

* 함수는 괄호\(\)를 사용해 호출할 코드 문장들을 모아두는 곳임. 함수를 실행할 때 괄호 안에 매개변수를 전달할 수 있어 함수 안의 문장에서 특정한 값에 접근하도록 만들 수 있음.

### Function\(\) 매개변수

* Function\(\) 생성자는 매개변수를 무한정 가질 수 있지만, 마지막 매개변수는 항상 함수의 몸체를 구성할 코드를 나타내는 문자열이어야 함. 생성자에 전달하는 그 밖의 매개변수는 함수 안에서 사용할 수 있으며 여러 매개변수를 전달할 때는 매개변수 사이를 쉼표로 구분해야 함.
* Function\(\) 생성자를 사용하는 방식은 자바스크립트의 eval\(\)을 사용해 함수 몸체가 도리 문자열을 해석하기 때문에 그리 추천할 만한 방법은 아님. 많은 경우에 eval\(\)은 불필요한 부하만 증가시킴. 만약 이 방식을 사용하고 있다면 코드 설계에 결함이 있을 확률이 매우 높음.
  * eval\(\) 의 문제점 : 보안 문제와 연결\(누군가 함부로 손댄 코드를 실행시키게 될 수도 있기 때문.\)
* Function\(\) 생성자를 사용할 때는 new 키워드가 있으나 없으나 결과가 같음.
* Function\(\) 생성자를 직접 호출하면 클로저가 생기지 않음.

### Function\(\) 속성과 메소드

#### 속성\(예: Function.prototype;\)

* prototype

### Function\(\) 객체의 인스턴스 속성과 메소드

#### 인스턴스 속성\(예: var myFunction - function\(x, y, x\) {}; myFunction.length;\)

* arguments
* constructor
* length

#### 인스턴스 메소드\(예: var myFunction = function\(x, y, z\) {}; myFunction.toString\(\);\)

* apply\(\)
* call\(\)
* toString\(\)

### 함수는 항상 값을 반환한다

* 함수 내부에서 반환할 값을 설정하지 않으면 undefined가 반환됨. 모든 함수는 항상 값을 반환함. 심지어 명시적으로 값을 반환하는 코드가 없을 때도 반환함. 명시적으로 반환값을 설정하지 않았을 때는 항상 undefined가 반환됨.

```javascript
var yelp = function() {
    console.log('I am yelping!');
}

// 함수는 우리가 명시적으로 값을 반환하지 않는 경우에도 항상 값을 반환하기 때문에 여기서는 true가 기록됨.
console.log(yelp === undefined);
```

### 함수에 매개변수 전달하기

```javascript
var addFunction = function(number1, number2) {
    var sum = number1 + number2;
    return sum;
};

// 6이 기록됨.
console.log(addFunction(3, 3));
```

### this와 arguments

* 함수라면 무엇이든 스코프/몸체 내부에서 this와 arguments를 사용할 수 있음. arguments 객체는 함수로 전달된 매개변수를 저장하고 있는 배열 비슷한 객체임. 다음 코드에서 우리는 함수를 정의할 때 매개변수를 깜빡 잊고 설정하지 않았지만 arguments 배열을 사용해 함수에 전달된 매개변수에 접근할 수 있었음.

```javascript
var add = function() {
    return arguments[0] + arguments[1];
}

console.log(add(4, 4));    // 8을 반환함.
```

* this 키워드는 함수를 포함하고 있는 객체에 대한 참조임. **알다시피 객체의 속성으로 포함된 함수\(즉, 메소드\)에서는 this를 사용해 "부모" 객체를 참조할 수 있음.** **함수를 전역 스코프에서 정의했으면 this의 값은 전역 스코프 객체\(웹 브라우저의 window\)가 됨.** 아래 코드를 살펴보고 this가 무엇일지 확인해 보자.

```javascript
var myObject1 = {
    name: 'myObject1',
    myMethod: function() {console.log(this);}
};

myobject1.myMethod();    // 'myObject1'이 기록됨.

var myObject2 = function() {console.log(this)};

myObject2();    // window가 기록됨.
```

### arguments.callee 속성

* arguments 객체에는 callee라는 속성이 있음. 이 속성은 현재 실행 중인 함수의 참조인데, 함수 스코프에서 실행 중인 함수를 참조할 때 사용되는\(예: arguments.callee\), 말하자면 자기 참조 속성임. 다음은 arguments.callee 속성을 사용해 호출한 함수의 참조를 얻는 코드임.

```javascript
var foo = function foo() {
    console.log(arguments.callee);    // foo()가 호출됨.
}
```

### 함수 인스턴스의 length 속성과 arguments.length

* arguments 객체에는 고유한 length 속성이 포함되어 있음. 속성 이름만 봤을 때는 함수 선언 시 정의된 인수의 개수를 알려줄 꺼 같지만, 사실 length 속성은 함수를 실행할 때 실제로 함수에 전달된 매개변수의 개수를 저장하고 있음.

```javascript
var myFunction = function(z, s, d) {
    return arguments.length;
}

console.log(myFunction());    // 함수에 전달된 매개변수가 없으므로 0이 기록됨.
```

* Function\(\) 인스턴스는 모두 length 속성을 포함하고 있음. 이 속성을 사용하면 함수선언 시 정의된 매개변수의 개수를 알 수 있음.

```javascript
var myFunction = function(z, s, d, e, r, m, q) {
    return myFunction.length;
}

console.log(myFunction());    // 7이 기록됨.
```

### 함수 매개변수 재정의

* 함수의 매개변수는 함수 내부에서 바로 혹은 arguments 배열을 사용해 재정의될 수 있음.

```javascript
var foo = false;
var bar = false;

var myFunction = function(foo, bar) {
    arguments[0] = true;
    bar = true;
    console.log(arguments[0], bar);    // true, true가 기록됨.
}

myFunction();
```

### 함수 완료 전에 반환하기\(실행 종료\)

* return 키워드를 사용하면 함수 실행 중 언제라도 동작을 취소할 수 있음. 이 때 반환할 값을 설정하지 않아도 상관없음. 다음 코드에서 add 함수는 매새변수가 정의되지 않았거나 숫자가 아니면 동작을 취소해 버림.

```javascript
var add = function(x, y) {
    // 매개변수가 숫자가 아니면 에러를 반환한다.
    if (typeof x !== 'number' || typeof y !== 'number') {
        return '숫자를 전달하세요';
    }
    
    return x + y;
}

console.log(add(3, 3));        // 6이 기록됨.
console.log(add('2', '2'));    // '숫자를 전달하세요'가 기록됨.
```

**return 키워드를 사용하면 함수 실행 중 언제든 함수 실행을 취소할 수 있음.**



### **함수를 정의하는 세 가지 방법**

* 함수는 함수 생성자, 함수 선언문, 함수 표현식 세 가지의 다른 방식으로 정의할 수 있음. 다음 코드는 이 세 가지 방식을 사용해 함수를 정의함.

```javascript
// 함수 생성자 : 마지막 매개변수는 함수의 로직(몸체 코드)부분이며, 그 외의 매개변수는 인수다.
var addConstructor = new Function('x', 'y', 'return x + y');

// 함수 선언문
function addStatement(x, y) {
    return x + y;
}

// 함수 표현식
var addExpression = function(x, y) {
    return x + y;
}
```

### 함수를 호출하는 네 가지 패턴

* 함수로서
* 메소드로서
* 생성자로서
* appply\(\) 혹은 call\(\)을 사용해서

```javascript
// 함수패턴
var myCunction = function() {
    return 'foo';
}

console.log(myFunction());    // 'foo'가 기록된다.

// 메소드 패턴
var myObject = {myFunction: function() {return 'bar';}};
console.log(myObject.myFuncton());    // 'bar'가 기록된다.

// 생성자 패턴
var Cody = function() {
    this.living = true;
    this.age = true;
    this.gender = 'male';
    this.getGender = function() {
        return this.gender;
    }
}

var cody = new Cody();    // Cody 생성자를 통해 호출된다.
console.log(cody);        // cody 객체와 속성이 기록된다.

// apply() 와 call() 패턴
var greet = {
    runGreet: function() {
        console.log(this.name, arguments[0], arguments[1]);
    }
};

var cody = {name:'cody'};
var lisa = {name:'lisa'};

// runGreet 함수가 마치 cody 객체의 메소드인 것처럼 호출한.
greet.runGreet.call(cody, 'foo', 'bar');    // cody foo bar 가 기록된다.
greet.runGreet.apply(lisa, ['foo', 'bar']);    // lisa foo bar 가 기록된다.

// call() 과 apply() 차이점은 호출할 함수에 매개변수를 전달하는 방식이다.
```

### 익명 함수

```javascript
function() {
    console.log('hi');    // 익명함수지만 실행하진 않았다.
}
// 우리가 전달할 익명 함수를 실행할 함수를 만든다.
var sayHi = function(f) {
    f();
}

// 익명 함수를 매개변수로서 전달한다.
sayi(function(){console.log('hi'});    // 'hi'가 기록된다.
```

### 자기 호출 표현식

함수 표현식은 괄호 연산자를 사용하면 정의하자마자 곧장 실행할 수 있다. sayWord\(\) 와 같은 형식을 자기 호출 함수라 한다.

```javascript
var sayWord = function() {
    console.log('Word 2 yo mo!');
}();

// 'Word 2 yo mo!' 가 기록된다.
```

### 자기 호출 익명 함수

스스로 호출되는 익명 함수 선언문도 만들 수 있는데, 이를 가리켜 자기 호출 익명 함수라 한다. 다음은 여러 익명 함수를 만든 후 만들자마자 바로 함수를 호출하는 코드이다.

```javascript
// 실제로 가장 많이 사용되고 / 볼 수 있는 형태
(function(msg) {
    console.log(msg);
})('Hi');

// 살짝 다르지만 같은 역할을 하는 코드
(function(msg) {
    console.log(msg);
}('Hi'));

// 가장 코드를 적게 쓸 수 있는 방식
!function sayHi() {console.log('hi');}();

// 모두 'Hi'가 기록된다.
```

### 함수는 중첩될 수 있다

함수를 다른 함수 안에 중첩해서 정의할 수 있으며 중첩 단계에 제한은 없다. 다음 코드에서 우리는 foo함수 안에 bar 함수를 만들고 그 안에 goo 함수를 정의했다.

```javascript
var foo = function() {
    var bar = function() {
        var goo = function() {
            console.log(this);    // window 머리 객체의 참조가 기록된다.
        }();
    }();
}();
```

### 함수에 함수 전달하기 / 함수에서 함수 반환하기

함수에 함수를 전달할 수 있다. 함수를 인수로 받거나 반환하는 함수를 가리켜 "교차함수"라고 한다. 다음의 코드에서 우리는 foo 함수에 익명함수를 전달하였으며 foo 함수는 전달받은 익명함수를 즉시 반환한다. 반환된 익명함수는 bar 변수에 저장된다.

```javascript
// 함수에 함수를 전달하거나 함수에서 함수를 반환할 수 있다.
var foo = function(f) {
    return f;
};

var bar = foo(function() {console.log('Hi')});

bar();    // 'Hi'가 기록된다.
```

따라서 bar를 호출하면 foo\(\) 함수에 전달된 익명 함수가 호출된다. 즉 foo\(\) 함수가 반환한 익명 함수 bar 변수에 참조된 것이다. 이를 통해 다른 값과 마찬가지로 함수도 함수에 전달할 수 있다는 것을 알 수 있다.

### 함수가 정의되기 전에 함수를 호출하기\(함수 호이스팅\)

함수는 실제로 함수가 정의되기 전에도 호출할 수 있다. 이러한 특성을 익혀두어서 잘 활용하거나 최소한 이런 동작을 만났을 때 이유 정도는 알고 있어야 한다. 다음 코드에서 sayYo\(\)와 sum\(\) 함수를 정의하기 전에 함수를 호출했다.

```javascript
// 예제 1
var speak = function() {
    sayYo();    // sayYo()는 아직 정의되지 않았지만 호출할 수 있다. 'yo'가 기록된다.
    function sayYo() {
        console.log('Yo');
    }
}();

// 예제 2
console.log(sum(2, 2));    // 아직 정의되지 않은 sum()을 호출한다. 
function sum(x, y) {
    return x + y;
}
```

자바스크립트는 코드를 실행하기 전에 함수 선언문을 먼저 해석하고 먼저 실행 스택/컨텍스트에 추가한다. 그래서 어디서 코드를 실행하든 항상 함수가 정의된 듯 동작한다. 함수를 사용할 때는 이러한 특성에 주의를 기울여야 할 것이다.

**"함수 표현식"으로 정의 함수는 호이스트 되지 않는다. "함수 선언문"만 호이스트 된다.** 

```javascript
addExpress(); 
// 함수 표현식
var addExpresss = function(x, y) { return x + y;}

// 에러를 발생시킴!!!! 함수 표현식은 호이스트 되지 않기 때문에.

```

### 함수는 자신을 호출할 수 있다\(재귀 호출\)

```javascript
var countDownFrom = function countDownFrom(num) {
    console.log(num);
    num--;    // 매개변수의 값을 수정한다.
    if (num < 0) {
        return false;    // num < 0이면 재귀 호출을 하지 않는다.
    }
    countDownFrom(num);
}

countDownFrom(5);
```

