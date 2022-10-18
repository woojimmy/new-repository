---
title: "[CSS] 기초 이론 - Font Style"
excerpt: "CSS에서 Font Style을 적용하는 방법을 알아보자. - wecode 사전스터디."

categories: 
  - HTML_CSS
tags: [CSS, theory, style, wecode]
toc: true
author_profile: true 
sidebar:
   nav: "docs"
---
>이 게시글은 wecode의 [사전스터디]과정을 통해 학습한 자료를 토대로 작성되었다.

<br>

# CSS - Font Style
## <span style="color:cornflowerblue">**Font Style 적용 방법**</span>
### <span style="color:cornflowerblue">**Font Family(글꼴)**</span>
`font-family`는 font 종류를 지정하는 property(속성)이다.
```css
#title {
    font-family: Georgia, "Times New Roman", Times, serif;
}
```
위 코드를 해석하면
- 브라우저에서 Georgia라는 font-family를 지원하면  Georgia font 적용
- Georgia font를 지원하지 않으면 "Times New Roman"을 적용
- "Times New Roman"을 지원하지 않으면 Times font를 적용
- 앞의 세 font가 모두 없으면 serif라는 font를 적용한다는 뜻이다.

여기서 property인 **font-family**에서 가장 가까운 값부터 순차적으로 적용되는 것을 알 수 있다. 사용자가 어떠한 브라우저를 사용하는지 모르기 때문에 여러 폰트를 입력한다. 가장 마지막에 위치한 'serif'는 모든 브라우저에서 지원하는 폰트이다.
><span style="color:crimson">위 코드에서 **"Times New Roman"** 만 쌍따옴표(`" "`)로 감싸져 있다. 이는 font 이름에 띄어쓰기가 있을 때는 `" "`로 감싸야하기 때문이다.</span>

---
### <span style="color:cornflowerblue">**Font Size(글자 크기)**</span>
`font-size`는 font 크기를 지정하는 property(속성)이다. Font 크기 단위는 `px`, `em`, `pt` 등 여러가지가 있으며, 주로 `px`를 많이 쓰지만 적지 않아도 된다.
```css
#title {
    font-size: 30px;
}
```
<br> 

그렇다면 크기가 정해진 `<h1>~<h6>` 같은 tag와 CSS 값 중에 어느것이 우선적으로 작동할까?
```css
h1 {
  font-size: 30px;
}

h4 {
  font-size: 50px;
}
```
원래대로라면 `<h1>`의 font size는 `<h4>`보다 커야한다. 그렇지만 위처럼 CSS 코드를 입력하면 `<h4>`의 font size가 더 크게 나타난다. 이는 <span style="color:crimson"><b>`해당 tag`나 `class`, `id`에 CSS값이 있다면 해당 스타일을 더 우선순위로 적용하기 때문이다.</b></span>

---

### <span style="color:cornflowerblue">**Font Weight(글자 두께)**</span>
`font-weight`는 font의 두께를 지정하는 property(속성)이다.
```css
#title {
    font-weight: bold;
}
```
- 값에 `nomal`, `bold`같은 문자 외에 `100`, `200`, ... ,`900` 등의 디테일한 숫자를 삽입할 수 있다.
- `400`과 `nomal`은 동일한 두께이다.
- `700`과 `bold`는 동일한 두께이다.

---

### <span style="color:cornflowerblue">**Font Style(글자 스타일)**</span>
`font-style`을 이용하여 font의 스타일을 변경할 수 있다.
```css
#title {
    font-style: Italic;
}
```
위 코드는 _Italic_ 체로 설정한다는 의미이다. 원하는 style이 있으면 구글링해서 위 property에 값으로 입력하면 된다.

---

### <span style="color:cornflowerblue">**Font Color(글자 색)**</span>
`color`는 font의 색을 지정하는 property(속성)이다. `color`를 지정하는 방식은 대표적으로 4가지가 있다. 4가지 방법을 알아보되 **예시는 모두 같은 색**으로 하겠다.<br> 
>예시 색상: <span style="color:green">green</span>, <span style="color:lightsalmon">lightsalmon</span>

CSS에서 색은 다음 사이트를 참고하면 더 여러가지 색을 입력할 수 있어 큰 도움이 된다.<br>
<a href="https://www.w3.org/wiki/CSS/Properties/color/keywords" target="_black">**CSS 색상 사이트로 이동(클릭)**</a>

#### Color Text(Color Name)
누구나 알아보기 쉬운 색(ex:yellow, green, blue etc...)을 지정하는 방법이다.
```css
#title {
    color: green;
}

.profile {
    color: lightsalmon;
}
```

#### Hex code(hex 색상코드)
6자리 문자와 숫자로 이루어진 색상코드이다. 별도의 접두사 없이 `color`라는 property에 입력하면 된다.<br> (Hash(`#`)는 본래 hex 색상코드에 포함되어 있으므로 같이 입력한다.)
```css
#title {
    color: #008000; /*green의 hex code*/
}

.profile {
    color: #ffa07a; /*lightsalmon의 hex code*/
}
```

#### RGB
RGB값을 `color: rgb(  )`에서 괄호(`( )`)안에 입력한다.
```css
#title {
    color: rgb(0,128,0); /*green의 rgb 값*/
}

.profile {
    color: rgb(255,160,122); /*lightsalmon의 rgb 값*/
```

#### hsl
hsl은 색상, 채도, 명도(hue, saturation, lightness)로 표현하는 색상이다. RGB와 비슷하게 `color: hsl(  )`의 괄호(`( )`) 안에 hsl값을 입력하면 된다. 입력시 단위를 주의한다.`( , %, %)`
```css
#title {
    color: hsl(120,100%,25%); /*green의 hsl*/
}

.profile {
    color: hsl(17,100%,74%); /*lightsalmon의 hsl*/
```

---

<br><br>
<br>
>Font style에 대해 알아봤다. Font style 코드는 주로 html에 작성했었는데, 이제 CSS에서 작성하는 습관을 길러야겠다.