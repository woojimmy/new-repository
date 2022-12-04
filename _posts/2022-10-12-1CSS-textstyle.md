---
title: "[HTML&CSS] 기초 이론 - Text Style"
excerpt: "HTML과 CSS에서 Text Style을 적용하는 방법을 알아보자."

categories: 
  - HTML_CSS
tags: [HTML, CSS, theory, style]
toc: true
author_profile: true 
sidebar:
   nav: "docs"
---

<br>

# Text Style

## <span style="color:cornflowerblue">**CSS에서 Text Style 적용 방법**</span>
CSS에서의 text style을 먼저 알아보자.

### <span style="color:cornflowerblue">**Text-Align(문자 정렬)**</span>
Text align은 '왼쪽 정렬', '가운데 정렬', '오른쪽 정렬'이 있다. property 이름은 `text-align`이고 값은 **left, center, right**이다.
```css
.left {
  text-align: left;
}
.center {
  text-align: center;
}
.right {
  text-align: right;
}
```
`text-align` 값이 없으면 왼쪽 정렬을 기본으로 한다. 그러나 위의 property를 입력해도 정렬이 안되는 tag가 있다. 다음 코드를 살펴보자
```html
<p class="right">오른쪽 정렬</p>  <!--1번-->
<span class="right">span의 오른쪽 정렬</span>  <!--2번-->
```
```css
.right {
    text-align: right;
}
```
위는 HTML, 아래는 CSS 코드이다. 이와같은 코드를 브라우저에 입력하면 `1번 코드`는 오른쪽 정렬이 되지만, `2번 코드`는 정렬되지 않는다. 이는 `<span>` tag가 `inline-element`이기 때문에 `<p>` tag와 차지하고 있는 영역이 다르기 때문이다.<br>
위 코드를 브라우저에 러닝하면<br><br>
<img src="/assets/images/20221012/align.png"><br><br>

이러한 형태로 브라우저에 나타나고, 여기서 각 코드가 차지하는 영역을 표시하면 <br><br>
<img src="/assets/images/20221012/textalign.png"><br>

이렇게 나타난다. `<p>` tag는 text가 적힌 줄 전체를 영역으로 차지하기 때문에 오른쪽 정렬씨 줄의 제일 오른쪽 끝으로 이동하지만, `<span>` tag는 content가 포함된 영역만을 차지하므로 줄에서 오른쪽 정렬이 나타나지 않는다.

---
### <span style="color:cornflowerblue">**Text-Indent(들여쓰기)**</span>
`text-indent`을 이용하여 CSS로 들여쓰기를 할 수 있다.
```css
#title {
    text-indent: 50px;
}
```
HTML 코드에서는 아무리 스페이스와 엔터를 추가해도 실제 브라우저에서 적용되지 않는다. 그렇기 때문에 CSS에서 `text-indent`라는 property에 값을 입력하면, 그 값만큼 들여쓰기가 실행된다.

---

## <span style="color:cornflowerblue">**HTML에서 Text Style 적용 방법**</span>

### <span style="color:cornflowerblue">**Blockquote(인용문)**</span>
인용문을 입력하기 위해서는 `<blockquote>` tag를 사용한다.
```html
<blockquote> JavaScript는 객체 기반의 스크립트 프로그래밍 언어이다.</blockquote>
```
브라우저는 `<blockquote>` tag 양쪽에 여백을 넣는 기본 스타일을 자동으로 적용한다.

---
### <span style="color:cornflowerblue">**Space(띄어쓰기)**</span>
HTML에서 띄어쓰기를 입력하기 위해 space를 여러번 추가하여도 하나의 space만 적용된다. 만약 다수의 space를 입력하려면 `&nbsp;`를 content에 추가하면 된다.<br>
(이 부분은 Javascript와 관련된 내용이다.)
```html
<p>스페이스 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;넣는 방법</p>
```

---
