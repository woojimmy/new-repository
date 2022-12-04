---
title: "[CSS] 기초 이론 - Box Sizing"
excerpt: " CSS에서 Box Sizing이 무엇인지 알아보자."

categories: 
  - HTML_CSS
tags: [CSS, theory]
author_profile: true 
sidebar:
   nav: "docs"
---

<br>

# CSS - Box sizing

## <span style="color:cornflowerblue">**Box Sizing이 필요한 이유**</span>
Box sizing을 얘기하기 전에, 먼저`margin`과 `padding`에 대해 알아야 한다. <br> (게시글 링크: <a href="https://woojimmy.github.io/html_css/2CSS-margin/" target="_blank">[CSS] - Margin % Padding</a>)<br>
Box sizing이 필요한 이유를 알아보기 위해 다음 코드들을 작성하고 실행해보자.<br>

[HTML 파일]<span style="color:darkgrey">(편의상 body tag만 작성하겠다.)</span>
```html
<body>
    <div class="first">
      첫 번째 박스, 가로 300px
    </div>
    
    <div class="second">
      두 번째 박스, 나도 가로 300px
    </div>
</body>
```
[CSS 파일]
```css
.first {
    width: 300px;
    margin-bottom: 20px;
}

.second {
    width: 300px;
    margin-bottom: 20px;
    padding: 50px;
    border-width: 10px;
}

div {
    background-color: yellow;
}
```
위 코드를 입력하고 실행하면<br>
<img src="/assets/images/20221012/boxsizing.png"><br>

분명 `first`와 `second`모두 `width`를 **300px**로 동일하게 설정하였지만 실제로 브라우저에 나타나는 크기가 다르다.<br> 그 이유는 `second`에는 `padding`값이 설정되어 있기 때문이다.
- `second`의 CSS를 보면 border-width(테두리 두께) 10px, padding(테두리 안 여백) 50px이 설정 되어있다.
- 각각의 값이 좌, 우 총 2번씩 반영되기 때문에 `second`의 실제 width는 **420px**이 된다.<br>
  > <span style="color:cornflowerblue">**300px(width) + (2 X 10px(border 좌, 우)) + (2 X 50px(padding 좌, 우)) = 420px**</span>

이러한 특성을 파악해 코딩하면 될 것 같지만, 디자인 시안에는 보통 전체 width만 나와있고, 개발자는 직접 padding을 계산하여 CSS를 적용해야 하는 불편함이 발생한다.<br> 

---

## <span style="color:cornflowerblue">**Box Sizing Property**</span>
이를 편리하게 개선하기 위해 `box-sizing`이라는 property를 개발해냈다.
```css
div {
    box-sizing: border-box;
}
```
위 코드를 예시의 CSS파일에 적용 후 실행해보자.
```css
.first {
    width: 300px;
    margin-bottom: 20px;
}

.second {
    width: 300px;
    margin-bottom: 20px;
    padding: 50px;
    border-width: 10px;
}

div {
    background-color: yellow;
    box-sizing: border-box;    /* 추가된 코드 */
}
```
<img src="/assets/images/20221012/boxsizing2.png"><br>

아까와 달리 `first` `second` 두 block 모두 같은 width로 나타난 것을 볼 수 있다.<br> 이처럼 `box-sizing` property는 여러 block의 사이즈를 맞추는 것에 특화되어 있어 매우 편리한 기능이다.
<br>

---
## <span style="color:cornflowerblue">**모든 Tag에 적용 방법**</span>

그런데 만약 여러 tag에 모두 `box-sizing`를 걸어야 한다면? 모든 tag를 CSS에 작성해야 할까?<br> 우리는 이럴 경우 selector(선택자)를 **`*`**으로 설정하는 것으로 문제를 해결할 수 있다.
```css
* {
    box-sizing: border-box;
}
```
위 코드를 CSS에 삽입하면 된다.
