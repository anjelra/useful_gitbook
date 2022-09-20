# sass

css 전처리기로 웹페이지에서는 읽을 수 없어서 css로 변환해야 한다. 변환을 하기 위해 자동화 도구를 사용할 수 있는데 그 중 하나가 gulp 이다.

### gulp

{% embed url="https://programmingsummaries.tistory.com/356" %}

* gulp는 node 기반이기 때문에, 반드시 node가 깔려 있어야 한다.

### sass 설치

* homebrew가 설치가 되어 있다면, brew install sass/sass/sass
* sass --version 

### gulp-sass 설치\(gulp로 sass를 compile 할 수 있도록 도와주는 모듈\)

* npm install gulp-sass --save-dev

### sass 문법

{% embed url="https://grace-go.tistory.com/57" %}

### css와 scss 의 차이점

#### 1. 주석

* css로 컴파일 했을 경우에는 한줄 주석은 컴파일 되지 않고, /\*\*/ 블럭 처리한 주석만 컴파일이 된다.

#### 2. 변수

* 변수 선언을 해서 사용할 수 있다.
* global변수와 local 변수가 있음.\(global 변수는 모든 영역에서 사용 가능하고, local 변수는 해당 소과로 안에서만 사용 가능.\)
* 변수 선언 뒤에 !default 라고 붙이면 해당 변수를 사용하지 못하게 한다.

#### 3. 연산자\(계산\)

* 값에 직접 계산을 넣을 수 있다. css 파일에서는 계산된 결과값으로 표기된다. css에서는 직접 계산을 넣으면 안되고, calc 함수를 사용해야 한다.
* 변수에 연산을 넣을 수 있다.\( ex: $box-width: \(200px - 100px\) \* 3 / 2; \)

#### 상속 & import\(가족\)

* @extend 선택자\(똑같은 내용을 그대로 받는다.\)
* @import "variable.scss";

#### 믹스인\(mixin\): @mixin 믹스인이름\(변수속성값\);

* 상속과 비슷하지만 태그를 사용하지 않고 믹스인을 만드는 것과 argument를 이용해 몇몇의 속성값을 원하는대로 쓸 수 있다는 점이 다르다.

```css
$control-margin: 10px;

@mixin afriends($bg-color) {
    width: 100px;
    height: 100px;
    margin: $control-margin;
    background: $bg-color;
}

.al {
    @include afriends(red);
}

.a2 {
    @include afriends(blue);
}
```

#### 함수

```css
@function randomName($width, $number) {
    @return $width / $number;
}

.function {
    width: randomName(1000px, 10);
    height: 200px;
    background: red;
}
```

### sass 변환 스타일

* nested \(기본값\)

```css
ul {
    font-family: Georgia;
    color: #333;}
    ul li {
        display: inline-block;
    }
```

* expanded

```css
ul {
    font-family: Georgia;
    color: #333;
}

ul li {
    display: inline-block;
}
```

* compact \(선언이 여러개 있어도 줄바꿈을 하지 않습니다.\)

```css
ul {font-family: Georgia; color: #333;}
ul li {display: inline-block;}
```

* compressed \(불필요한 공백을 모두 제거합니다.\)

```css
ul{font-family:Georgia;color: #333;}ul li{display:inline-block;}
```

### scss 문법

* 변수 선언

```css
$white: #fff;
```

