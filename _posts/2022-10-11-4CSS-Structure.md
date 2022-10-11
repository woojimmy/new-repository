---
title: "[CSS] 기초 이론 - CSS의 개념과 구조"
excerpt: "CSS의 정의, 구조 그리고 HTML에 적용하는 방법을 알아보자. - wecode 사전스터디."

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

# CSS
## <span style="color:cornflowerblue">**CSS란?**</span>
> <span style="color:cornflowerblue">**CSS(Cascading Style Sheet)**</span>는 '마크업 언어'가 실제 표시되는 방법을 기술하는 **스타일 언어(Style Sheet Language)**이다. HTML와 XHTML에 주로 쓰이며, 레이아웃과 스타일을 정의할 때 자유도가 높다.<br> 마크업 언어(ex:HTML)가 웹사이트의 몸체를 담당한다면 **CSS**는 옷과 액세서리처럼 꾸미는 역할을 담당한다. 즉, HTML은 그대로 두고 CSS파일만 변경해도 전혀 다른 웹사이트처럼 꾸밀 수 있다.<br> <span style="color:darkgrey">(출처: 위키백과: CSS)</span>

HTML만으로도 사이트를 만들 수 있지만, 화려한 웹 사이트를 만드려면 HTML과 CSS가 뗄 수 없는 관계입니다. **HTML**이 header, paragraph, table 등으로 정보를 조직화하는 구조를 제공한다면, **CSS**는 HTML이 아름다워 보이도록 스타일을 입히는 것이다.

---
## <span style="color:cornflowerblue">**CSS의 적용방법**</span>
CSS를 HTML에 적용하는 방법은 3가지가 있다.
### 인라인 스타일(Inline Style)
Tag의 style attribute에 직접 작성이 가능하다.
```html
<h1 style="color:red;">Frontend</h1>
```
Inline style을 사용하면 다음과 같은 장단점이 존재한다.
- 빠르고 편리하다.
- 그러나 적용해야할 style이 많아지면 가독성이 떨어진다.
- HTML tag와 style 코드가 혼재되어 유지보수에 좋지 않다.

아래 예시를 보면 단점을 이해하기 쉽다.
```html
<h1 style="color: red; font-size: 30px; background-color: yellow; font-weight: bold;">Frontend</h1>
```

---
### style Tag
HTML 파일 내에 CSS 부분을 구분하여 작성하는 방법이다. <span style="color:cornflowerblue">`<style> </style>`</span> tag 사이에 CSS 문법을 사용하여 스타일을 작성한다.
```html
<style>
  h2 {
    color: #408090;
  }
</style>
```
- HTML 파일에 HTML 코드와 CSS를 함께 작성하는 편리하고 빠른 방법이다.
- 가능적으로 HTML 코드와 분리되지 않기 때문에 유지보수에 적합하지 않다.

---
### CSS 파일 작성
HTML파일과 분리하여 CSS파일을 따로 작성하는 방법이다. 보통 <span style="color:cornflowerblue">**`style.css`**</span>라는 파일을 만들어 사용한다.(CSS의 확장자는 `.css`이다.)<br> 분리된 CSS파일을 HTML파일에 적용하기 위해 연결해주는 tag는 다음과 같다.
```html
<link href="style.css" rel="stylesheet" type="test/css" />
```
위 tag를 살펴보면
1. `<link>` : 사용할 CSS파일을 연결해주는 tag
2. `href` : href 속성에 CSS파일 경로를 작성
3. `rel` : HTML파일과 CSS파일의 관계를 설명하는 attribute이다. CSS파일을 연결하기 위해서는 항상 그 값으로 **"stylesheet"** 를 입력해야 한다.
4. `type` : `<link>` tag로 연결되는 파일을 알려준다. 여기서 CSS파일을 연결하므로 **"text/css"** 값을 입력한다.
   
---
## <span style="color:cornflowerblue">**CSS의 작성 방법**</span>
별도로 작성한 CSS파일과 HTML파일의 연결을 완료했다면, 이제 <span style="color:cornflowerblue">`style.css`</span>파일에서 CSS를 어떻게 작성하는지 알아보자. <br> 
```css
h2 {
  color: red;
  font-size: 30px;
}
```
위 코드는 `<h2>` tag의 content(text)를 <span style="color:crimson">**빨간색**</span>으로 바꾸고, 글자 크기를 **30px**로 설정한다는 뜻이다. 각각의 줄을 속성(attribute)이라고 하며, 세미콜론(`;`)으로 구분하여 여러 attribute를 부여할 수 있다.<br>
위 코드를 하나하나 살펴보면
- `<h2>`: <span style="color:cornflowerblue">**선택자(Selector)**</span>라고 하며 해당 tag를 선택하거나, `class`또는 `id`값이 올 수도 있다.
- `color`, `font-size`: <span style="color:cornflowerblue">**속성(property)**</span>이라고 한다. 변경하고 싶은 항목을 지칭한다.
- `red`, `30px` : 각 'property'의 값이다.

---
## <span style="color:cornflowerblue">**Selector 이름 적용 방법**</span>
Tag, class, id 등 각 이름마다 Selector를 CSS파일에 적용하는 방법이 다르다.
### Tag Name
HTML의 tag는 그 tag명만 적으면 적용된다.
```css
p {
  font-size: 16px;
} 

a {
  background-color: yellow;
}
```
예시 중 위의 코드는 모든 `<p>` tag에 폰트 크기를 16px로, 아래 코드는 모든 `<a>` tag에 배경을 노란색으로 설정하는 CSS 코드이다.

---
### .className
HTML에서 `class`를 통해 이름을 부여한 tag는 **selector**로 지정할 때 이름 앞에 <span style="color:cornflowerblue">**dot(`.`)**</span>를 입력한다.<br> 만약 HTML 파일에 이러한 코드가 있다고 하자.
```html
<p class="profile">이름</p>
<span class="profile">직업</span>
<div class="profile">한마디</div>
```
여기에 **"profile"** 이라는 `class`가 적용된 태그에 모두 두꺼운 글씨를 설정하고 싶다면, 다음과 같은 코드를 CSS파일에 입력하면 된다.
```css
.profile {
  font-weight: bold;
}
```

---
### #idName
HTML에서 `id`를 통해 이름을 부여한 tag는 **selector**로 지정할 때 이름 앞에 <span style="color:cornflowerblue">**hash(`#`)**</span>를 입력한다. `id`는 하나의 파일에서 오직 1번만 사용 가능하다는 것을 주의해서 HTML 코드를 작성해보자.
```html
<div id="myprofile"> 내 프로필</div>
```
이 **"myprofile"** 이라는 `id`가 적용된 태그에 원하는 CSS 스타일을 적용하기 위해선 CSS파일에 다음과 같은 코드를 입력한다.
```css
#myprofile {
  border-width: 1px;
  border-color: black;
  border-style: solid;
  text-align: center;
}
```

---


<br><br>
<br>
>드디어 CSS 첫 글이다. 다음에는 폰트 스타일을 CSS로 적용하는 방법을 알아보자.