---
description: 제 9장
---

# Array\(\)

### Array\(\) 객체의 사용

배열은 값을 순서대로 나열한 목록이며, 일반적으로는 0부터 시작하는 숫자 색인값을 통해 포함된 값을 훑을 목적으로 배열을 작성한다. 객체도 값을 포함하기는 하지만, 배열은 값을 순서대로 나열하여 각 값에 해당하는 숫자 색인이 있는 반면 객체는 값에 해당하는 속성 이름만 있을 뿐 값 사이에 순서가 없다는 점이 다르다. 따라서 배열에서는 숫자를 검색키고 사용하나 객체에서는 사용자가 정의한 속성 이름을 사용한다. 사실 자바스크립트에는 진정한 의미의 연갈 배열이 없다. 하지만 객체를 사용하면 연관 배열과 같은 기능을 제공할 수 있다.

```javascript
var myArray = ['blue', 'green', 'orange', 'red'];

console.log(myArray[0]);    // myArray에 색인번호 0으로 접근하여 blue를 기록한다.

// 다음을 비교
var myObject = {    // 자바스크립트의 객체는 연관 배열 또는 해시로도 사용할 수 있다.
    'blue': 'blue',
    'green': 'green',
    'orange': 'orange',
    'red': 'red'
};

console.log(myObject['blue']);    // blue가 기록된다.
```

* 배열에는 어떤 값도 저장할 수 있으며 저장된 값은 언제든 수정하거나 삭제할 수 있다.
* "해시\(hash\)"\(연관 배열이라고도 함\)가 필요하다면 객체가 가장 현실적인 대안이다.
* Array\(\)는 특별한 형식의 Object\(\)이다. 다시 말해, Array\(\) 인스턴스는 기본적으로 Object\(\) 인스턴스와 같으며, 여기에 몇 개의 기능만 추가됐을 뿐이다.\(예: length 속성과 숫자 색인\)
* 일반적으로 배열에 포함된 값을 원소라 부른다.

### Array\(\) 매개변수

Array\(\) 생성자에는 배열 인스턴스에 포함될 값을 전달할 수 있으며 각 값은 쉼표로 구분한다. 하지만 만약에 Array\(\)  생성자에 한 개의 매개변수만 전달하고 매개변수가 숫자값이라면 생자는 이를 배열의 크기로 이해하고 해당 크기의 배열을 만든다. 단, 이때 배열에는 아무 값도 저장되지 않으므로 색인을 사용해 접근하면 모든 값이 정의되지 않은 상태로 나타난다.\(undefined\)

```javascript
var foo = new Array(1, 2, 3);
var bar = new Array(100);

console.log(foo[0], foo[2]);    // '1 3'이 기록된다.
console.log(bar[0], bar.length);    // 'undefined 100'이 기록된다.
```

### Array\(\) 속성과 메소드

Array\(\) 객체는 다음과 같은 속성과 메소드를 포함한다.\(상속받은 속성과 메소드는 제외\).

#### 속성

* prototype

### Array 객체 인스턴스의 속성과 메소드

#### 인스턴스 속성\(예: var myArray = \['foo', 'bar'\]; myArray.length;\)

* constructor
* index
* input
* length

#### 인스턴스 메소드\(예: var myArray = \['foo'\]; myArray.pop\(\);\)

* pop\(\)
* push\(\)
* reverse\(\)
* shift\(\)
* sort\(\)
* splice\(\)
* unshift\(\)
* concat\(\)
* join\(\)
* slice\(\)

### 배열 만들기

대부분의 자바스크립트 객체와 마찬가지로 배열 객체 역시 new 키워드와 Array\(\) 생성자를 같이 사용해 만들 수 있으며 리터럴 문법을 사용해 만들 수도 있다.

```javascript
// Array() 생성자
var myArray1 = new Array('blue', 'green', 'orange', 'red');

console.log(myArray1);    // ["blue", "green", "orange", "red"]가 기록된다.

// 배열 리터럴 표기법
var myArray2 = ['blue', 'green', 'orange', 'red'];
console.log(myArray2);    // ["blue", "green", "orange", "red"]가 기록된다.

```

### 배열에 값을 추가하고 갱신하기

배열에 어디에든 언제든지 값을 추가할 수 있다.

```javascript
var myArray = [];
myArray[50] = 'blue';
console.log(myArray.length);    // 51이 기록됨. 자바스크립트는 0번부터 "blue" 라는 값을 가진 50번 색인까지 값을 만들어 넣으므로 51이 기록된다.
```

잠시 자바스크립트의 동적인 특성과 자바스크립트가 자료형을 강하게 강제하지 않는 언어라는 사실을 떠올려 보자. 이러한 특성 덕분에 자바스크립트에서 배열의 값은 언제든 수정할 수 있다. 아래 코드는 50번 색인에 있는 값을 객체로 변경하는 코드다.

```javascript
var myArray = [];
myArray[50] = 'blue';
myArray[50] = {'color': 'blue'};    // 자료형을 문자열에서 Object()로 바꾼다.
console.log(myArray[50]);    // Object {color="blue"}가 기록된다.

// 각 괄호를 사용해 배열의 색인과 color 속성에 접근한다.
console.log(myArray[50]['color']);    // 'blue'가 기록된다.

// 점 표기법을 사용한다.
console.log(myArray[50].color);        // 'blue'가 기록된다.
```

### 크기와 색인

배열은 0부터 색인을 시작한다. 

```javascript
var myArray = ['blue'];
console.log(myArray[0]);    // 'blue'가 기록된다.
console.log(myArray.length); // 1이 기록된다.
```

### 미리 설정한 크기로 배열 만들기

```javascript
var myArray = new Array(3);
console.log(myArray.length);    // 3이 기록된다.
console.log(myArray[0]);        // undefined가 기록된다.

// 그러면 한 개의 숫자값만 포함하는 배열은 어떻게 만들 수 있을까?
var myArray = [4];    // 리터럴 형식을 사용하면 된다.
```

### 배열의 크기를 설정하면 값을 추가하거나 제거할 수 있다

```javascript
var myArray = ['blue', 'green', 'orange', 'red'];
console.log(myArray.length);    // 4가 기록된다.

myArray.length = 99;
console.log(myArray.length);    // 99가 기록된다.

myArray.length = 1;
console.log(myArray[1]);    // undefined가 기록된다.

console.log(myArray);    // ["blue"]가 기록된다.
```

### 다른 배열을 포함한 배열\(다중 배열\)

배열 안에 다른 배열이 포함된 경우를 가리켜 다중 배열이라고 부른다. 다중 배열에 접근하려면 각괄호를 연이어 사용하면 된다.

```javascript
var myArray = [[[['4번째 배열']]]];
console.log(myArray[0][0][0][0]);    // '4번째 배열'이 기록된다.
```

### 배열을 앞뒤로 훑

배열을 훑을 수 있는 가장 간단한 방법은 while 반복문을 사용하는 것이다.

```javascript
var myArray = ['blue', 'green', 'orange', 'red'];

var myArrayLength = myArray.length;    // 배열의 크기를 저장해 불필요한 탐색을 방지한다.
var counter = 0;

while (counter < myArrayLength) {
    console.log(myArray[counter]); // 순서대로 기록된다.
    
    counter++;
}
```

```javascript
var myArray = ['blue', 'green', 'orange', 'red'];

var myArrayLength = myArray.length;    // 배열의 크기를 저장해 불필요한 탐색을 방지한다.

while (myArrayLength--) {
    console.log(myArray[myArrayLength]);
}
```



