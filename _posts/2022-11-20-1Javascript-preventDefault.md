---
title: "[Javascript] - Event.preventDefault"
excerpt: "Jacascript에서 .preventDefault의 기능을 알아보고 페이지 이동이 되지 않는 문제를 해결해보자."

categories: 
  - Javascript
tags: [Javascript]
toc: true
author_profile: true 
sidebar:
   nav: "docs"
---

# Event.preventDefault

## 문제점
instagram을 클론한 'westagram'이라는 사이트를 만드는 중이다. <br> 로그인 페이지와 메인(게시글) 페이지를 만든 후, 로그인 페이지에서 ID와 Pw input field에 조건에 충족하는 ID, Pw를 입력한 뒤에 로그인 버튼이 색이 바뀌며 활성화 <br> -> 버튼 클릭 시 로그인 페이지에서 메인 페이지로 이동. <br> 이러한 동작을 구현 중인데, 문제가 발생했다.
<video type="video/mp4"  src="/assets/images/20221120/Westagramloginvideo1.mp4" width="100%">

</video>