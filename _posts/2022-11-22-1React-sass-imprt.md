---
title: "[React] - .scss file import 위치"
excerpt: "React에서 .scss 파일을 import하는 위치와 이유를 알아보자"

categories: 
  - React
tags: [react, scss, css, import]
toc: true
author_profile: true 
sidebar:
   nav: "docs"
---

# Sass

## Sass란?
> **Sass (Syntactically Awesome Style Sheets)**는 CSS preprocessor 중 하나로, 여러 가지 기능들을 문법적으로 편리하게 작성할 수 있도록 제공하는 **preprocessor의 양식에 맞게 파일을 작성**하고, 최종적으로 browser에 실행 전 처리를 통해 읽을 수 있는 CSS파일로 변환해주는 기능을 한다.

## Scss
Sass에는 2가지 방식이 있다. 바로 `.scss`와 `.sass` <br/>
`.scss`는 `.sass`와 비교해서
- 엄격하지 않은 들여쓰기
- CSS의 문법에 존재하는 세미콜론, 괄호 등을 사용하는 CSS와 유사성
- 기존의 CSS Project에 Scss파일을 import하여 새 코드만 더하면 되는 편리성 등의 특징을 가지고 있다. <br/><br/>

*scss와 sass의 차이점 보러 가기 ->*<a href="https://www.geeksforgeeks.org/what-is-the-difference-between-scss-and-sass/">  geeksforgeeks- SCSS and SASS </a><br>

## 왜 CSS가 아닌 Scss를 쓸까?
현재 React로 만들고 있는 instagram clone page를 CSS 파일을 사용해서 열어보자. <br>
<img src='/assets/images/20221122/sass1.png'>
<br>
?? layout이 모두 깨져있다.
<br>
왜 깨졌는지 알아보기 위해 개발자도구로 저 찌그러진 facebook 로고를 클릭해보자 <br><br>
<img src='/assets/images/20221122/sass2.png'>
<br>

분명 내가 연 창은 Login 페이지인데, Main 페이지의 css파일인 `ma.css`가 함께 적용되어 `width`값이 틀어졌다. 
<br>
이것은 React는 SPA를 지원해 하나의 html에 여러 stylesheet가 한 번에 적용되어 생기는 문제이다. 
<br>
그렇기 때문에 React에서 우리는 CSS파일이 아닌 Scss의 `nesting`, `variable` 등의 특징을 이용해 이러한 stylesheet의 충돌을 방지하는 것이다.
<br>

<img src='/assets/images/20221122/sass3.png'>
<br>
`nesting`으로 Login 페이지와 Main 페이지의 style을 구분해서 충돌을 방지한 모습
<br><br>

## Scss의 import
일반적인 scss 파일은 React의 js파일에 import해준다. 코드는 다음과 같다
```javascript
import ' scss 파일의 경로 ';
```
<span style="color:crimson">(세미콜론(`;`)을 붙이지 않으면 error가 발생하므로 주의)</span>
<br>

일반적으로 Scss파일은 js파일에 import해준다.
<br><br><br>

## 변수 Scss 파일의 import
단, 내가 이해하기 어려웠던 부분은 변수를 선언하는 `variable.scss`, `mixin.scss`는 위와 같은 방식으로 import시 error가 발생한다. 
<br>
<img src='/assets/images/20221122/sass4.png'>
<br>
이해하지 못한 이유는 아래와 같다. 
<br>
- React는 SPA를 지원하므로 모든 stylesheet가 함께 적용된다.
- `variable.scss`와 `mixin.scss`를 js파일에 import한다.
- 선언한 변수들 또한 stylesheet에 포함될 것이다.
- 다른 Scss 파일에 변수를 참조해도 가능할 것이다.

이게 내가 생각했던 것인데, 현실은 변수가 undefined라는 error가...
<br><br>

왜 이러는지 알아보기 전에 정상적으로 import하는 방법부터 찾아보자.
<br>
답은 간단했다.
```scss
@import ' variable.scss 또는 mixin.scss 파일의 경로';
```
위 코드를 <span style="color:cornflowerblue">**js파일이 아닌 여기 선언된 변수를 참조하는 다른 Scss 파일에 삽입**</span>해야 한다. 
<br>
즉, js파일에 import하는 것이 아니라 다른 Scss 파일에 import해야 하는 것이다.<br>
이와 같은 방법으로 import하면 변수 참조가 제대로 작동하고, error가 사라지는 것을 알 수 있다.

### error 이유
왜 js에 import하는 것은 안되고, scss끼리 import할 때만 되는지, 그 경로와 이유가 궁금했다.
<br>
그런데 내가 간과한 사실이 있다.
<br>
Sass는 CSS가 아닌, browser가 읽을 수 있는 CSS 형태로 전처리 해주는 preprocessor라는 것.
<br>
Sass는 standard가 아니기 때문에 .scss 파일에서 선언하는 변수는 browser가 읽을 수 없는 것이다.
<br>
그렇기 때문에 .scss 파일에 .scss 파일을 import하여 변수에 대한 값 또는 함수를 먼저 참조한 후,
<br>
이를 CSS로 전처리해야 browser가 읽을 수 있는 CSS가 되는 것이다.
<br>
간단해 보이는 이유지만 CSS와 Sass의 차이를 명확히 구분하지 못했던 것 같다.<br><br>


Sass의 주 기능들에 대해 잘 나와있는 사이트 링크 하나 올리고 마치겠다.
<br>
틈틈히 읽어 Sass를 더 잘 다루게 연습하자.
<br>
<a href="https://sass-lang.com/guide">Sass Guide</a>