---
title: "[HTML] 기초 이론 - HTML의 Attribute"
excerpt: "Attribute의 구조 및 개념과 id, class 2가지 Attribute의 차이점을 알아보자."

categories: 
  - HTML_CSS
tags: [HTML, theory, attribute]
toc: true
author_profile: true 
sidebar:
   nav: "docs"
---

<br>

# HTML 속성(Attribute)
## <span style="color:cornflowerblue">**HTML 속성(Attribute)이란?**</span>
Attribute를 설명하기 위해 코드 하나를 예시로 들어보겠다
```html
<a href="https://woojimmy.github.io/">블로그 이동</a>
```
- `<a>`는 tag의 이름이다.
- `href`는 `<a>` tag의 **attribute(속성) 이름**이다.
- `"https://woojimmy.github.io/"`는 `href` 속성에 대한 **attribute 값**이다.
- `블로그 이동`은 content(내용)이다.

---
<br>
Attribute는 각각의 tag마다 사용할 수 있는 attribute가 정해져 있다. 위 예시로 적은 '링크' 코드에서 `<href>`는 다른 페이지로 이동하는 주소를 가리키기 때문에 `<div>`같은 tag에는 사용할 수 없다.<br> 주로 사용하는 tag와 attribute가 있기 때문에 이를 익힌다면 금방 익숙해질 수 있다.

---

## <span style="color:cornflowerblue">**id, class Attribute**</span>
### id
 `id`는 각 tag에 이름을 부여하는 attribute이다. 그러나 웹 페이지에서 해당 `id` attribute는 오직 1가지 이름만이 가질 수 있다.<br> (중복 이용 불가능)
```html
<div id="profile">
</div>
```
위 코드에서 `profile`이라는 값을 가진 `id`를 더이상 사용할 수 없게 된다.<br>
`id`는 보통 해당 element에만 넣고 싶은 디자인을 적용할 때 사용한다. 예를 들어, `<p>` tag에 font-size를 20px로 적용한다면, 해당 페이지의 모든 `<p>` tag의 font-size가 변경된다. 만약 디자인이 반영되기 원하는 `<p>` tag에 `id`를 설정해주면 설정된 `<P>` tag만 변경된다.

---
### class
`class` 또한 tag에 이름을 부여하는 속성이다. 그러나 `id`와의 차이점은 `class`는 여러 tag에 중복된 이름을 부여할 수 있다는 것이다.
```html
<div class="content">블라</div>
<p class="content">블라블라</p>
```
이처럼 `class`를 사용하면 같은 웹 페이지 안에 중복된 이름을 가진 attribute를 설정할 수 있다.

---

## <span style="color:cornflowerblue">**여러 Attribute 추가**</span>
예시
```html
<div id="profile" class="content">블라</div> 
<img src="bla.png" alt="사진" target="_blank"> 
```
이처럼 하나의 tag에 여러 attribute를 부여하는 것이 가능하다. attribute는 순서는 상관없이 써도 된다.

---

<br><br>
<br>
>사실 Attribute는 CSS에서 Attribute Selector 등으로 다시 다뤄야한다. 그렇기에 이번엔 간단한 개념과 구조만 다뤄 글이 짧고 내용이 단순해졌다. 공부하는 틈틈히 내용을 보충해야겠다.