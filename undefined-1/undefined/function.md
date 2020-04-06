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

