---
title: "[Project] 여행 후기를 담은 정적인 페이지(2) - Header"
excerpt: "나의 첫 번째 개인 프로젝트."

categories: 
  - Project
tags: [project, personal_project, static]
toc: true
author_profile: true 
sidebar:
   nav: "docs"
---
## 결과
<img src="/assets/images/20221020/headercomplete.png">
<img src="/assets/images/20221020/headercompletemini.png">

## 무엇을 했는가?
- screen 사이즈 변경시 네비게이션 위치 변경(`flex`이용)
- 제목을 포함해 모든 문구 클릭시 페이지 내 알맞은 위치(`section`)로 이동하게 링크
- 네비게이션에 마우스를 올리면 포인터 변경과 스타일(컬러, 밑줄) 변경

## 무엇을 알았는가?
### <nav> Tag
상단 목록을 작성할 때 `<nav>`태그를 사용했다. `<nav>`가 어디 쓰이는거지??
- 원래는 `<div>`를 이용했었다.
- 둘 다 여러 태그를 하나의 구조로 만드는 태그이다.
- `<nav>`는 **시맨틱 태그(Semantic Tag)**로 태그안에 content 유추가 쉽다.
- 그러므로 상단 네비게이션 바는 알기 쉽게 `<nav>`를 사용하자

### 양 옆 여백
<img src="/assets/images/20221020/header1.png"><br>
원래였음 `<h1>`태그인 왼쪽 문구와 `<nav>`태그인 오른쪽 문구에 각각 왼쪽 padding, 오른쪽 padding을 줬을것이다. <br> 그런데 한방에 해결하는 방법이 있었다!. header의 class인 `container`에 `width`와 `margin`을 이용해서 여백을 넣을 수 있었다!
```css
.container {
    display: flex;
    align-items: center;
    justify-content: space-between;
    width: 90%; /* 이거 추가 */
    margin: auto; /* 이것도 추가 */
}
```
<img src="/assets/images/20221020/header2.png"><br> 간단히 성공!

### 버튼 클릭시 같은 페이지에서 이동
그동안 궁금했었다. 상단 네비게이터를 클릭했을 때, 다른 html페이지가 아닌, 같은 페이지에서 해당 section으로 이동하는걸 어떻게하는지..<br> 여러 사이트의 elements를 뒤져보다 알았다! 어떤 section에 id를 설정하고, 링크로 그 아이디를 입력하는 것이었다. `<a>`태그에 링크를 `#id이름`을 걸어주면 이동하는 것을 발견했다!!! <br> 아직 `section`들을 만들기 전이라 간단하게 만들어주고 `height`를 많이 줘서 크기를 늘렸다. 그리고 각 `section`별로 id를 입력하고 이 id를 상단 네이게이터에 각각 링크했더니, 클릭할 때마다 페이지가 이동하는 것을 확인할 수 있었다!!

### header의 height 위치
창 크기에 따라 latout을 변경할거기에 header에 `height`값을 주고 싶었다. 그런데 `<header>`태그에 줘야할지 그 자식으로 다른 요소(ex: `<h1>`, `<nav>`, `<li>` 등..)를 감싼 `<div>`태그에 넣어야할지 혼란스러웠다. <br> 실제 직접 `height`값을 넉넉히 주고 입력해보니 정렬이 있었다.
<img src="/assets/images/20221020/header3.png"><br>`<header>`에 줬을 때.<br>
<img src="/assets/images/20221020/header4.png"><br>`<div>`에 줬을 때.<br>
미묘하지만 정렬의 차이가 있다. `<header>`는 글자 기준 아래만 늘어난 느낌이면, `<div>`는 글자가 전체적으로 가운데로 정렬했다. 후자가 더 깔끔해보여서 후자로 가기로 했다.

---

다음엔 본문에 section을 나누어 꾸밀것이다. <br> 가장먼저 보이는 기본 페이지부터 꾸미자