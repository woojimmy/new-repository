---
title: "[HTML] 기초 이론 - HTML정의와 용어"
excerpt: "HTML이란 무엇인지 알아보고, HTML에 관련된 기초 용어들(Tag, Content, Attribute, Element)들을 알아보자 - wecode 사전스터디."

categories: 
  - HTML
tags: [HTML, theory, wecode]
toc: true
author_profile: true 
sidebar:
   nav: "docs"
---
>이 게시글은 wecode의 [사전스터디]과정을 통해 학습한 자료를 토대로 작성되었다.

<br>

# HTML
## <span style="color:cornflowerblue">**HTML이란?**</span>
> <span style="color:cornflowerblue">**HTML(Hyper Text Markup Language)**</span>는 웹 페이지 표시를 위해 개발된 '마크업 언어'이다. HTML은 제목, 단란, 목록 등과 같은 본문을 위한 구조적 의미를 나타내는 것뿐만 아니라 링크, 인용과 그 밖의 항목으로 구조적 문서를 만들 수 있는 방법을 제공한다. 그리고 이미지와 객체를 내장하여 대화형 양식으로 생성하는 데 사용될 수 있다. HTML은 웹 페이지 콘텐츠 안의 꺽쇠괄호(`< >`)에 둘러싸인 **태그(Tag)**로 되어있는 HTML 요소 형태로 작성한다. <br> <span style="color:darkgrey">(출처: 위키백과: HTML)</span>

HTML은 간단히 말해서 다음과 같은 정의와 기능을 가지고 있다.
<ul><b>
<li>HTML은 웹 페이지를 만들기 위한 언어이다.</li>
<li>HTML로 웹페이지의 구조를 잡을 수 있다.</li>
<li>HTML 파일은 이미지, 텍스트, 비디어, 버튼 등 웹사이트에 보여줄 내용을 구성하고 있다.</li>
<li>브라우저(safari, chrome, ie...)는 HTML 파일을 바탕으로 웹 페이지를 생성한다.</li>
</b></ul>

---
## <span style="color:cornflowerblue">**HTML 확장자**</span>
HTML 파일의 확장자는 <span style="color:cornflowerblue"><b>.html</b></span> 을 사용한다.<br>
<div style="text-align: center;"><img src="/assets/images/20221011html/html.png"></div>
<br>

---

## <span style="color:cornflowerblue">**HTML 필수 태그(Tag)**</span>
HTML 파일에 필요한 최소한의 tag는 아래와 같다.
```html
<html>
    <head>
        <body>
        </body>
    </head>
</html>
```
HTML 파일은 위 tag들을 필수적으로 포함하고 있어야 웹 브라우저에서 정상적으로 작동될 수 있다.<br>
<span style="color:darkgrey">(`<!DOCTYPE>`같은 경우 tag가 아니기 때문에 위에 삽입하지 않았다.<br> 이 내용은 [HTML 기초 이론 - HTML Tags] 게시글에서 다룰 예정이다.)</span>

---

## <span style="color:cornflowerblue">**HTML 용어**</span>


tag와 관련하여 HTML 기초 용어(tag, content, attribute, element)를 알아보도록 하자.


### 태그(Tag), 내용(Content)
tag는 아래처럼 꺽쇠괄호(`< >`)로 감싸져 있다.
```
<태그이름>내용</태그이름>
```
<ul>
<li>브라우저에서 태그(tag)는 나타나지 않고 내용(content) 부분만 보여준다.</li>
<li>내용(content)을 기준으로 왼쪽이 <b>시작 태그(opening tag)</b>이고, 오른쪽에 있는 것이 <b>종료 태그(closing tag)</b>이다. </li>
<li>종료 태그(closing tag)에는 <b>/(slash)</b>가 있다.</li>
</ul>

tag 중 아래와 같은 tag는 opening tag, closing tag가 존재한다.
```html
<p></p>
<h1></h1>
<h2></h2>
<a></a>
```
반면, 시작과 동시에 종료되어 opening tag와 closing tag가 구분없는 tag도 존재한다.
```html
<img>
<br>
```
---
### 속성(Attribute)
속성(attribute)은 opening tag에 위치하며, 한 tag에 여러 attribute를 지정할 수 있다.
```html
<div class="title">시작~</div>
<a href="https://www.naver.com">네이버</a>
<img src="Hi.png" alt="안녕 사진">
```
위 코드에서 `div`, `a`, `img`는 <span style="color:cornflowerblue">**tag**</span>이고, `class`, `href`, `src`, `alt`는 <span style="color:cornflowerblue">**attribute**</span>이다.

---
### 요소(Element)
opening tag로 시작하여 closing tag로 끝나고 그 사이에 content가 있는 구조를 <span style="color:cornflowerblue">**요소(element)**</span>라고 한다. closing tag가 필요없는 것은 tag 자체로 element가 된다.
```html
<h1>시작~</h1> <!-- 해당 줄 전체가 element-->
<img src="start.png"> <!--tag 자체가 element-->
```
---

<br><br>
<br>
>이번엔 HTML에 대해 알아봤다. 다음은 HTML의 tag들에 대해 다뤄봐야겠다.