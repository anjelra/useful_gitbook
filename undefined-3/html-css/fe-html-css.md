---
description: (변대리님 교육을 통해 얻은 지식)
---

# FE 개발자가 꼭 알아야 하는 html

#### language 선언은 반드시 해야 한다.

```markup
<head lang="ko">
```

lang 속성은 웹 접근성에 관한 내용이다. 웹 콘텐츠 접근성 지침\(KWCAG\) 2.1에는 웹페이지의 head 요소 안에 페이지의 기본 언어 선언을 규정하고 있기 때문에 필히 명시되어야 한다.

#### viewport란?

웹페이지가 사용자에게 보여지는 영역을 말함. viewport는 반응형 웹\(responsive web\)을 고려해야할 때 주로 사용함. 반응형 웹이란 하나의 웹사이트로 데스크탑 PC, 스마트폰, 태블릿 PC 등 접속하는 디스플레의의 종류에 따라 화면의 크기가 자동으로 변하도록 만든 웹 페이지를 말함. 미디어 쿼리는 css3부터 지원이 되는  css기술로 미디어 타입, 화면 크기 등을 기준으로 다른 스타일 시트를 적용할 수 있도록 해줌. 이를 이용해서 화면 크기가 변할 때 스타일을 바뀌도록 해서 반응형 웹을 구현할 수 있음. 

css 는 rendering block resource\(렌더링 차단\)에 포함되어 있어서 media query로 분기쳐서 성능을 향상 시킬 수 있음.

```markup
<meata name="viewport" content="width=device-width, initial-scale=1.0">
```

* width=device-width : 페이지의 너비를 기기의 스크린 너비로 설정함. 즉, 렌더링 영역을 기기의 뷰포트의 크기와 같게 만들어줌.
* initial-scale=1.0 : 처음 페이지 로딩시 확대/축소가 되지 않은 원래 크기를 사용하도록 함. 0~10 사이의 값을 가짐.
* mininum-scale : 줄일 수 있는 최소 크기를 지정. 0~10 사이의 값을 가짐.
* maximum-scale : 늘릴 수 있는 최대 크기를 지정. 0~10 사이의 값을 가짐.
* user-scalable: yes 또는 no 값을 가지며 사용자가 화면을 확대/축소 할 수 있는지를 지정.

{% embed url="https://developers.google.com/web/fundamentals/performance/critical-rendering-path/render-blocking-css" %}



#### 비표준모드, 표준모드

* doctype이 표준이냐 비표준이냐를 가늠하는 것은 랜더링방식. 브라우저가 처음 html 을 읽을 때 doctype을 보고 렌더링 방식을 결정.
* 표준모드는 누가 결정하는가? 

  * wac에서 지정한 표준 doctype을 따르는가
  * wac에서 지정한 웹표준을 따르는
  * 이 두가지 조건에 따라서 결정됨.

* 비표준은 h1\(heading tag\)을 한번만 써야함. h1 -&gt; h2 -&gt; h3 이런식으로 써야함. 건너뛸 수 없음.
* 표준은 section 태그는 무조건 h1이 있어야 하고, section 이 여러개 있다면 여러 개의 h1을 쓸 수 있음.

#### b 태그와 strong 태그

* b태그와 strong 태그는 모두 진하게 표현되므로 눈에는 똑같이 보임.
* 그러나 사용 용도가 명확히 다름.
* b 태그는 단지 텍스트를 굵게 하는 역할.
* strong 태그는 강조하기 위해서 사용.

#### button 태그와 a 태그 차이점

a 태그는 목적지가 있는 곳에만 사용을 해야 함. 예를 들어, 햄버거 메뉴 같은 경우에는 button 태그를 쓰는 것이 맞음.

#### 리스트

* ul\(unordered list\) : 순서없는 리스트
* ol\(ordered list\) : 순서있는 리스트
* dl : 설명을 할 때 사용. 정의 목록이라고도 함. 실무에서는 잘 사용하지 않음.

#### img 태그 사용시 주의할 점

```markup
<img src="" width="200">
```

width에 "200px" 이런 식으로 단위를 사용하면 안됨.

#### gif vs jpg vs png vs svg 차이

* `gif`: 256색으로 제한적이지만 용량이 작고, 애니메이션와 투명 이미지가 가능하다.
* `jpg`: 높은 압축률과 자연스러운 색상 표현이 가능하여 사진이나 일반적인 그림에 사용
* `png`: `jpg`와 비교했을 때, 이미지 손실이 없고 투명과 반투명 모두 지원한다.
* png, svg는 압축을 하지 않는다.
* gif 는 투명 이미지가 되지만 애니메이션이 된다.

{% embed url="https://medium.com/@soeunlee/web%EC%97%90%EC%84%9C-png-gif-jpeg-svg-%EC%A4%91-%EC%96%B4%EB%96%A4-%EA%B2%83%EC%9D%84-%EC%82%AC%EC%9A%A9%ED%95%98%EB%A9%B4-%EC%A2%8B%EC%9D%84%EA%B9%8C%EC%9A%94-6937300e776e" %}

#### 테이블 태그

* 테이블에서는 position을 쓸 수 없음\(지원을 안함\)
* &lt;thead&gt;, &lt;tfoot&gt; 는 생략 가능
* &lt;tbody&gt;가 1개만 있다면 생략 가능







#### 



