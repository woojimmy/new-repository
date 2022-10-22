---
title: "[CSS] - link방식과 @import방식의 차이"
excerpt: "HTML에 CSS를 연결하는 두 가지 방법. 'link 방식'과 '@import 방식'의 특징과 차이점을 알아보자."

categories: 
  - HTML_CSS
tags: [HTML, CSS, link, import]
toc: true
author_profile: true 
sidebar:
   nav: "docs"
---
# HTML과 CSS를 연결하는 두 가지 방법
지금 하고 있는 정적인 웹 페이지 만들기를 위해 여러 사이트와 블로그 글들을 구글링하던 중, `@import`라는 것이 보였다. 

## link와 @import가 무엇?
나는 그 동안 계속 CSS파일을 불러올 때 `link`를 써왔다.
```html
<link href="style.css" rel="stylesheet" type="text/css" />
```
내가 쓰는 CSS파일을 `link`하는 코드이다.
그런데 몇몇 글이나 사이트에서 `@import`를 쓰는 것을 보았고, 이 코드가 CSS파일들을 불러온다는 것을 알았다. 
```css
@import url("anotherstyle.css")
```
위와 같은 방식으로 CSS파일에 입력해서 CSS파일 안에 다른 CSS파일을 중첩하는 역할을 하기도 하고, `<style>`태그로 HTML파일에 직접 입력할 수도 있다.

##  무엇이 다른가??
가장 큰 차이점은 **로딩 방식**이다. `link`는 **병렬 로딩 방식**, `@import`는 **직렬 로딩 방식**이다.
```css
charset "utf-8";

@import "example1.css";
@import "example2.css";
@import "example3.css";
```
`@import`를 쓰게 되는 경우 `example1.css`를 불러온 다음에 `example2.css`, 그리고 그 다음에 `example3.css`를 로딩 하는 방식인 **직렬 로딩 방식**이다. 그렇기 때문에 CSS의 양이 방대해진다면, 전체 CSS를 로딩하는데 걸리는 시간이 매우 길어지게 된다.<br>

```html
<link href="example1.css" rel="stylesheet">
<link href="example2.css" rel="stylesheet">
<link href="example3.css" rel="stylesheet">
```
`link`를 쓰게되면 `example1.css`, `example2.css`, `example3.css` 세 가지 CSS파일을 모두 동시에 로딩하는 **병렬 로딩 방식**으로 진행된다. 그렇기 때문에 `@import`에 비해 CSS 로딩이 훨씬 빠르고 효율적이기 때문에, 현재 많은 웹 페이지에서 `link`의 비중이 높다.

## @import를 사용하는 경우는?
유저들이 많은 웹 페이지들이 주로 어떤 방식을 사용하는지 직접 개발자 도구로 CSS를 찾아보았다. <br> 대부분의 웹 페이지는 거의 `link`로만 이루어져 있는 것 같았다. 토스나 당근 같은 웹 페이지의 경우 모두 `link`로 되어 있었고(내가 발견하지 못한 것일수도 있지만.. 일단 `@import`는 못찾았다.), 우아한 형제들 채용 사이트의 경우 CSS파일 안에 `@import`가 있었지만, 각각의 CSS파일에 하나의 동일한 CSS(font 관련 CSS인것 같았다.)를 연결시켜 놓았었고, 결국 나머지 CSS들은 모두 `link`로 연결되어 있었다. <br> 코드를 보면 `@import`를 쓰는 것이 코드가 더 간결하고, 여러 CSS 스타일 시트를 하나의 CSS파일로 처리할 수 있으니 더 편리할 것 같지만, 실제 많은 글에서 `link`를 선호하는 것이 좋다고 나와있었다. 아무래도 잠깐의 딜레이만으로도 사용자는 불편함을 느낄 수 있는 웹 페이지 특성상 병렬 로딩 방식인 `link`가 더 유리하기 때문이라고 생각한다. <br> 그 중 오래된 브라우저에서는 버전의 문제로 `@import`를 지원하지 않아, CSS를 숨기는데 용이해 사용하기도 한다고 하는데, 최근 사용자들이 이용하는 웹 브라우저는 거의 모두가 `@import`를 지원하고 있어 더 깊이 알아보지는 않았다.
<br>
<img src="/assets/images/20221022/linkinput.png"> <br>
위 사진은 <a href="https://developer.mozilla.org/en-US/docs/Web/CSS/@import" target="_black">mdn</a>에 나와있는 `@import`의 브라우저별 호환성이다. 

## 엣지와 호환성??
많은 글에서 `@import`와 마이크로소프트 엣지 브라우저의 호환성 버그를 언급했다. 엣지 브라우저가 `@import`를 제대로 지원하지 않는다는 얘기가 많았는데, 위에 mdn자료에서 보듯이 엣지와 호환이 가능하다고 나와있다.<br>
<img src="/assets/images/20221022/linkinput2.png"> <br>
그래서 궁금해서 만들고 있던 웹 페이지에 `link`가 아닌 `@import`로 CSS를 연결시켜보기로 했다. <br>
<img src="/assets/images/20221022/linkinput3.png"> <br>
<img src="/assets/images/20221022/linkinput4.png"> <br> 위에서 아래로 바꾸로 Live server를 실행해 보았다. <br>
<img src="/assets/images/20221022/linkinput5.png"> <br> 음... 되는거 같지만... <br> 그래도 나는 정말 짧은 코드이고, 만약 방대한 양의 코드이거나 여러 스타일 시트를 연결한다면 버그가 생길 수 있기 때문에 섣불리 판단하지 말자. 이 부분은 진짜 그냥 궁금해서 해본거기 때문에 너무 의미 부여하지 않는걸로..ㅎㅎ

