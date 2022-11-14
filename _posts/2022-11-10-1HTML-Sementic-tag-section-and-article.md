---
title: "[HTML] Semantic Tag - Section과 Article의 차이"
excerpt: "HTML의 Semantic Tag 중 비슷해보이는 'section' tag와 'article' tag가 무엇이 다르고 어떻게 쓰이는지 알아보자."

categories: 
  - HTML_CSS
tags: [HTML, theory]
toc: true
author_profile: true 
sidebar:
   nav: "docs"
---

# Semantic Tag

## Semantic Tag를 사용하는 이유
`<section>`과 `<article>`의 차이 이전에 왜 semantic tag를 사용하는지 먼저 찾아봤다. <br><br>

non-semantic tag인 `<div>`나 `<span>`을 사용하면 코드를 만들 때 바로바로 만들 수 있을 것 같은데, 왜 굳이 하나하나 의미나 역할을 알아야하는 semantic tag를 쓰는걸 선호할까? <br> 내가 찾아본 이유는 다음과 같았다.

### 1. 검색엔진 최적화(SEO)
Semantic tag는 웹 페이지의 검색엔진 최적화(SEO, search engine optimization)를 도와 사용자가 쉽게 접근할 수 있게 도와준다고 한다. <br> 어떻게? <br> 
<!--<img src="/assets/images/20221111/semantic1.png"> <br>
Google 검색 센터에서 'Google 검색 개발 가이드'에 나와있는 내용이다. <br>
<a href="https://developers.google.com/search/docs/fundamentals/get-started-developers">Google 검색 센터 바로가기</a> <br> 윗 글에서 `의미론적 HTML 마
-->



 

2. 쉬운 소스코드 구조화
브라우저가 웹 문서의 소스 코드를 보고 어느 부분이 헤더인지, 어느 부분이 본문인지를 쉽게 알아낼 수 있다. 웹 문서를 분석하는 서비스 (ex. 스크린 리더기) 같은 것들이 있을 때 분석하기 용이해진다.

 

3. 코드 가독성 향상
여러 사람과 함께 작업을 할 때, 굳이 클래스를 지정하지 않아도 쉽게 어느 부분이 헤더 영역이고, 본문 영역인지 쉽게 알 수 있다. 그래서 유지보수를 하기도 쉬워진다.