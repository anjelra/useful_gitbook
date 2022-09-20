---
description: (변대리님 교육을 통해 얻은 지식)
---

# FE 개발자가 꼭 알아야 하는 css

## css (cascading style sheets)

#### cascading이란 무엇인가

cascading이란 '구체성'을 말한다. 즉, 효과를 적용받는 우선 순위를 나타낸다.

행렬을 생각하면 쉽게 이해할 수 있다.

|     0     |   0   |     0    |  0  |
| :-------: | :---: | :------: | :-: |
|     0     |   0   |     0    |  0  |
|     0     |   0   |     0    |  0  |
|     0     |   0   |     0    |  0  |
| important | #(id) | .(class) | tag |
|    짱!!    |  100점 |    3점    |  1  |

{% embed url="https://justmakeyourself.tistory.com/entry/cascading-using-css" %}

![같은 태그여도 body h1 이 더 구체적으로 선언했기 때문에 green 컬러가 먹을 것임.](<../../.gitbook/assets/image (1).png>)

![](<../../.gitbook/assets/image (37).png>)

#### block-level, inline-level의 차이점

* block-level : div 같은 무조건 100% width를 가지는 태그&#x20;
  * _일반적인 모든 요소 포함하며, `div, h1~h6, p, ul, li, table` 등_
* inline-level : span 처럼 딱 size 만큼만 width가 잡히는 태그&#x20;
  * _block 레벨의 자식요소이며, `span, i, img, em, strong` 등_

#### css  적용방식

* Inline (유지보수가 힘듦)

```css
<div style="..."> 내용 </div>
```

* Internal (우리 회사에서 패널에서 사용 하는 방식)

```css
<style>...</style>
```

* External (대부분 사이트에서 현재 많이 사용하고 있는 방식)

```css
<link rel="stylesheet" href="css/style.css">
```

* @import (절대 사용하면 안되는 방식)

```css
@import url('css/style.css');
```

#### 문서 구조 선택자

* 자손 선택

```css
div span { color: red; }
```

* 자식 선택자

```css
div > span { color: red; }
```

* 인접 형제 선택자

```css
div + span { color: red; }
```

주의할 점 : 선택자를 잡을 때 class 로 잡아야 한다.(div, span 등으로 잡으면 안됨)

#### 가상 선택자

* **가상 클래스 (미리 정의해놓은 상황에 적용이 되도록 약속되어있는 보이지 않는 클래스)**

:first-child, :last-child, :link(하이퍼링크이면서 아직 방문하지 않은 앵커), :visited(이미 방문한 하이퍼링크를 의미),  :focus, :hover, :active

* **가상 요소 (미리 정의해놓은 위치에 삽입이 되도록 약속되어있는 보이지 않는 요소)**

:before, :after, :first-line, :first-letter&#x20;

**input 태그에서는 가상요소(before, after 등 )를 사용할 수 없다.**

**여기서 한가지 주의사항!!** \
****before, after 가상 요소는 content: " " 가 있어야 생명력이 있음. 이 content를 없애고자 할 때에는 content: none 을 주면 됨.

#### **:first-child**

* 내가 부모 기준으로 무조건 첫번째 자식이어야 함. 결국 자기 자신을 뜻하는 거임.

```css
dt: first-child {
    background-color: red;
}    

<dl>
    <dt> 안녕 </dt>
    <dd> 하이 </dd>
</dl>
```

![이런 식으로 내가 원하는 모양이 나옴.](<../../.gitbook/assets/image (52).png>)

```css
dd: first-child {
    background-color: red;
}    

<dl>
    <dt> 안녕 </dt>
    <dd> 하이 </dd>
</dl>
```

![이런식으로 정상작동하지 않는다. 그 이유는, 부모인 dl 기준으로 dd가 첫번째 자식이 아니기 때문이다. 내가 헷갈렸던 부분을 해결해줘서 행복.](<../../.gitbook/assets/image (18).png>)

#### margin, padding, background, border는 상속이 되지 않음.(박스 모델 관련 속성들은 상속되지 않는다)

![](<../../.gitbook/assets/image (47).png>)

![](<../../.gitbook/assets/image (39).png>)

#### color, font-size, line-height는 상속이 됨.&#x20;

```css
<div>블라블라<em>히히</em></div>
```

이렇게 html 이 작성되어 있을 때, 상속이 되기 때문에 div에 color를 주는게 좋음.

#### reset을 쓰는 이유

* 사용자 에이전트 스타일을 없애기 위해 사용.
  * 사용자 에이전트를 예를 들면, ie, ms, safari 등의 브라우저에서 기본으로 css 먹인 스타일을 말함.

### 캐스케이드 규칙

1. 중요도(!important) & 출처&#x20;
2. 구체성
3. 선언순

#### 중요도(!important) & 출처

* 기본적으로 !important로 선언된 모든 규칙은 그렇지 않은 규칙보다 우선한다.
* 출처는 제작사, 사용자, 사용자 에이전트(User Agent)로 구분한다.

![](<../../.gitbook/assets/image (3).png>)

#### 구체성

```css
p#bright { color: silver; }
p { color: red; }

<p id="bright">Hello,CSS</p>
```

`정답은 silver`

#### 선언순서

```css
p { color: silver; }
p { color: red; }
```

`정답은 red`

#### \*\*헷갈리는 문제&#x20;

```css
div {
  width: 100px;
  height: 50px;
  border: 1px solid #222;
  background-color: red;
}

span {
  height: 50%;
  background-color: white;
}

<div>
  <span>히히</span>
</div>
```

`질문 : height: 50%는 몇 px 일까요??`

`정답 : inline인 span 은 width, height, padding 가질 수 없음.`

#### 태그의 블록요소와 인라인 요소

* block (위에서 아래로 쌓임)
  * div, table, p, h1, h2, h3 등등이 있음
* inline (옆으로 쌓임)
  * width, height를 가질 수 없음. padding 가능. margin은 가능하나 좌우 여백만 가능.
  * border는 가능함
* inline-block(옆으로 쌓임)
  * width, height, padding, margin을 다 사용할 수 있음.&#x20;
  * 자유자재로 하고 싶은 경우에는 inline-block 을 사용하면 됨.
* 팁: inline-block끼리 붙이면 여백이 3px 정도 생기는데, div에 font-size:0으로 주면 다 붙어서 여백을 잡을 수 있음.

{% embed url="https://junistory.blogspot.com/2017/07/html5.html" %}

#### [https://norux.me/63](https://norux.me/63)

####

#### 알아두어야 하는 em 단위&#x20;

```css
div {
    font-size: 16px;
}
p {
    font-size: 1.2em;
}
```

* 위에 처럼 css 가 선언되었다면, p는 16\*1.2px이 됨.
* &#x20;em은 자신의 부모를 보고 결정.
* rem은 root를 뜻함.
* html 의 body가 root이므로, body가 16px 이면, p는 16\*1.2px가 됨.
* em, rem은 반응형에 많이 쓰임.

#### css2, css3 지원 범위

* css2는 IE7부터 지원
* css3는 IE9부터 지원&#x20;

#### 레티나 개념에 대해 공부하시오.

#### background-repeat의 기본값은 repeat. no-repeat이라고 써줘야 no-repeat이 됨.

#### \*\*헷갈리는 문제

![히히를 가운데로 배치하려면?](<../../.gitbook/assets/image (9).png>)

1. inline-block요소를 이용하는 법&#x20;

```css
div {
  width: 100px;
  height: 50px;
  border: 1px solid #222;
  background-color: red;
   text-align: center;
}

span {
  height: 50%;
  background-color: white;
}


<div>
  <span>히히</span>
</div>
```

* span 태그가 inline-block이기 때문에  text-align: center 가 가능하다.(inline 요소도 가능)
* div 태그가 block 요소이기 때문에 block에  text-align: center를 주면 글자로 취급을 해서 가운데로 이동시키는게 가능하다.&#x20;

2\. block 요소를 이용하는 법

```css
div {
  width: 100px;
  height: 50px;
  border: 1px solid #222;
  background-color: red;
   text-align: center;
}

p {
  width: 50px;
  margin: 0 auto;
  background-color: white;
}

<div>
  <p>히히</p>
</div>
```

* p는 block 요소이기 때문에 width를 100%를 가진다.&#x20;
* 따라서, p 의 width를 정해주고, margin: 0 auto; 라고 주면 중앙정렬이 가능하다.

#### 기본값&#x20;

* width: auto
* height: auto
* min-width: auto
* min-height: auto
* position: static

#### position과 같이 알아야 하는 z-index

* static
* relative
* absolute
* fixed

z-index를 쓰고 싶다면 relative, absolute, fixed 가 되어야 z-index를 쓸 수 있다.

#### &#x20;position의 기준

* absolute의 기준은 부모의 relative
* fixed는 브라우저가 기준&#x20;

#### position의 속도

* 1등은 absolute. 그 이유는 단독으로 움직이기 때문이다.
* animation을 일으키는 요소가 있다면 absolute를 쓰는게 가장 좋다.

#### display: none 과 visibility: hidden 의 차이

* display: none
  * span 두개가 붙어 있다면 첫번째 span을 display: none을 이용해서 안보이게 하면 두번째 span이 당겨짐.
* visibility: hidden
  * 보이고 안보이고만 하는거라 위치의 영향이 없음.&#x20;
* visibility는 위치를 전부 계산해줘야 하기 때문에 display가 더 효율적임.

#### inline 요소에 float 속성을 주면 block 으로 바뀜.

#### font-family

* font-family: Helvetica, '돋움', sans-serif;
* 우선순위:       1,                2,            3 -> 없으면 다음꺼 그 다음꺼 이런식으로 됨.

#### 웹폰트

* 웹폰트는 사용하면 안됨.
* 브라우저 마다 확장자(.woff, .eob등이 있음)가 없으면 흰 화면이 보이기 때문에 안됨.

#### vertical-align

* inline, inline-block 인 경우에만 사용 가능.(table-cell은 예외)
* vertical-align은 친구따라 달라짐. 부모 기준이 아님.
  * 따라서, vertical-align으로 정렬하는 것은 좋지 않음.
  * vertical-align 은 주로 한줄짜리 인데 '아이콘, 글, 아이콘' 이런 식으로 정렬을 해야할 때 쓰는게 좋음.
  * 친구가 없으면 vertical-align을 사용할 수 없음. inline-block이여도.&#x20;

![](<../../.gitbook/assets/image (20).png>)

![](<../../.gitbook/assets/image (31).png>)

* vertical class에 중앙정렬을 하고 싶으면 친구와 부모의 높이가 있어야 함.
* 또한 body에도 height 100%가 먹여져 있어야 가능함.
* 또한, friend class에 display: inline-block을 준 이유는 span 은 inline 요소이므로 height를 가질 수 없음.
* 따라서 요소를 바꿔주고 높이도 지정을 해줘야 가능.

#### inline 속성을 block 으로 바꾸는 요소가 있음. inline 속성에 position->absolute, fixed를 주면 block으로 바뀜.

#### 팁!! 잘 모르겠으면 css에 background 를 채우면 한결 이해하기가 쉬워짐.

#### 중앙정렬 관련해서 참좋면 좋을 사이트

{% embed url="https://blog.logrocket.com/13-ways-to-vertical-center/" %}



```yaml
<div class="wrap_middle type01">
    <div class="wrap">
        <div class="inner">중앙정렬</div>
    </div>
</div>
```

### \*\* 가장 중요한 면접에 꼭 나올만한 것들 \*\*

1. 브라우저의 랜더 과정을 설명하시오.
2. 성을 향상시킬 수 있는 방법은 무엇일까요?
3. http
4. svg 특징.&#x20;
5. css는 3 depth 이상으로 안 쓰는게 좋음. 브라우저가 안에서 부터 읽기 때문에.





#### min-height, max-height 등은 height가 있으면 먹지 않음
