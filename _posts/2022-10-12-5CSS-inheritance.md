---
title: "[CSS] 기초 이론 - Inheritance & Grouping"
excerpt: " CSS에서 Inheritance & Grouping에 대해 알아보자. - wecode 사전스터디."

categories: 
  - HTML_CSS
tags: [CSS, theory, wecode]
toc: true
author_profile: true 
sidebar:
   nav: "docs"
---
>이 게시글은 wecode의 [사전스터디]과정을 통해 학습한 자료를 토대로 작성되었다.

<br>

# CSS - Inheritance & Grouping

## <span style="color:cornflowerblue">**상속(Inheritance)**</span>
상속은 CSS가 가진 특성이다.<br>
말 그대로 스타일이 **상속(inheritance)**되어 하위 tag에게도 같은 스타일이 적용되는 특성이다.<br>

```html
<body>
    Javascript

    <p>자바스크립트(영어: JavaScript)는 객체 기반의 스크립트 프로그래밍 언어이다.</p>

    <blockquote>다른 응용 프로그램의 내장 객체에도 접근할 수 있는 기능을 가지고 있다.</blockquote>
</body>
```
```css
body {
    color: red;
    font-size: 14px;
}

blockquote {
    color: green;
}
```
위 HTML, CSS 코드를 브라우저에서 실행하면 다음과 같이 나타난다.<br>
<div style="border: 2px solid black;">
 <img src="/assets/images/20221012/inheritance.png">
 </div>
<br>
`<body>` tag는 'red'라는 color값을 갖지만, `<p>` tag는 아무런 CSS 스타일을 갖고 있지 않아도 빨간색, 14px의 size로 나타난다.<br>
이는 부모(상위 tag)인 `<body>` tag의 스타일을 상속받았기 때문이다.<br>
그러나, 마지막에 `<blockquote>`부분은 `<body>`tag에 속함에도 초록색으로 글자가 나타난다. 이는 **inheritance**가 발생하지 않았다는 것을 의미한다.<br>
그 이유는 tag 본인이 property를 가지고 있는 경우, 부모의 property보다 본인의 것이 우선적으로 적용되기 때문이다.

---

## <span style="color:cornflowerblue">**그루핑(Grouping)**</span>
CSS에는 여러 selector에 동일한 스타일을 적용하는 방법이 있다.
```css
p {
    color: green;
}

blockquote {
    color: green;
}

div {
    color: green;
}
```
위 코드는 모두 같은 스타일을 가지고 있고, selector만 다르다.<br> 이러한 코드는 다음과 같이 하나의 코드에 작성할 수 있다.
```css
p, blockquote, div {
    color: green;
}
```
여러 selector를 나열하고, `,`로 각 selector를 구분해주면 된다.

---