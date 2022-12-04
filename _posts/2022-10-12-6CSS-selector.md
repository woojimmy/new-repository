---
title: "[CSS] 기초 이론 - 선택자(Selector)"
excerpt: " CSS에서 선택자(Selector)의 정의와 특징에 대해 알아보자."

categories: 
  - HTML_CSS
tags: [CSS, theory, selector]
toc: true
author_profile: true 
sidebar:
   nav: "docs"
---

<br>

# CSS - Selector

## <span style="color:cornflowerblue">**선택자(Selector)의 표현**</span>
아래 코드를 살펴보자
```css
p {
  font-size: 20px;
}
.pTag {
  color: gray;
}
#thirdLine {
  text-decoration: underline;
}
```
이 selector는 class나 id를 태그와 결합하여 작성할 수 있다.
```css
p.pTag {   /* -- 1번 selector -- */
  color: gray;
}
p#thirdLIne {   /* -- 2번 selector -- */
  text-decoration: underline;
}
```
'1번 selector'는 `p` tag이면서 `pTag` class이다.<br>
'2번 selector'는 `p` tag이면서 `thirdLine` id이다.<br>
<span style="color:cornflowerblue">**`p#third-line.p-tag`**</span>이러한 방법으로 작성도 가능하지만, **'tag+id+class'**의 조합은 과한 표현이다.<br>

---
## <span style="color:cornflowerblue">**특정 부모에 포함된 Selector 적용**</span>
```css
.pre span {
  background-color: yellow;
}
```
위 CSS에서 최종적으로 적용되는 selector는 `span`이다.<br>
그러나 모든 `span` tag가 아니라 **'pre'**라는 'class'의 내부에 있는 `span`에 적용되는 것을 의미한다.<br>

 <span style="color:crimson">여기선 selector가 서로 붙어있지 않고 space로 띄어쓰기가 있다는 점을 주의해야한다.</span><br> 만약 띄어쓰기 없이 붙어있으면 `pre` class와 `span` tag 모두 동일하게 작동하는 것을 의미한다.<br>
 
  위 CSS코드를 아래 HTML에 적용하여 브라우저에 실행하면
```html
<div class="pre">
  <span>이건 노란색 배경이고</span>
</div>
<div class="main">
  <span>이건 아님!</span>
</div>
<span class="pre">이것도 아님</span>
<div>
  <p class="pre">
    <span>이건 적용됩니다! 노란색배경!</span>
  </p>
</div>
```
<div style="border: 2px solid black;">
<img src="/assets/images/20221013/selectorhtml.png">
</div><br> 이처럼 나타난다. 'class'가 `pre`가 아니거나, `pre` class에 포함되지 않은 `span`은 적용되지 않는 것을 알 수 있다.

```css
.profile div .first .second span {
  background-color: lightsalmon;
}
```
이처럼 길게 작성할 수도 있다.<br> 여기서 의미는 `profile` class 밑에, `div` tag 밑에, `first` class 밑에, `second` class 밑에, `span` tag에 적용되는 것이다. <br>
> <span style="color:cornflowerblue">**.profile > div > .first > .second > <u>span</u>**</span> <--실제 적용되는 tag

---
## <span style="color:cornflowerblue">**Selector의 우선순위**</span>
```css
p {
  font-size: 30px;
}
.pTag {
  font-size: 15px;
}
```
```html
<p class="pTag">예에시</p>
```
위 코드들을 보면 `pTag` class를 적용한 tag가 `p`인데, 두 가지 모두 각자 다른 `font-size`의 property value를 갖는다.<br> 여기서 '예에시'라는 content는 어떠한 `font-size`값을 따라갈까?<br> 이를 알기 위해서는 selector표현의 **우선순위**를 알아야 한다.<br> 이 우선순위는 점수 계산으로 이루어 진다.

|  selector |    점수    |
|:----:|:------------:|
| inline styling<br> &nbsp;&nbsp;&nbsp;(html에 직적 style 요소 입력)&nbsp;&nbsp;&nbsp; |   &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 1000점 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;   |
| id |   100점   |
| class |   10점   |
| tag | 1점 | 

그렇다면 위 표를 참고해서 
```html
<p class="pTag">예에시</p>
```
이 코드의 우선순위를 살펴보자<br>
- `p` tag에 적용된 것은 '30px' : 1점
- `pTag` class에 적용된 것은 '15px' : 10점
- <span style="color:cornflowerblue">**점수가 더 높은 10점의 15px가 적용된다.**</span>

그렇다면 만약에 위 CSS에 다음과 같은 코드가 추가된다면 어떨까
```css
p.pTag {
  font-size: 100px;
}
```
다시 점수를 계산해보면
- `p` tag에 적용된 것은 '30px' : 1점
- `pTag` class에 적용된 것은 '15px' : 10점
- `p.pTag`는 `p` tag 1점 + 'pTag` class 10점 : 11점
- <span style="color:cornflowerblue">**점수가 가장 높은 11점의 100px가 적용된다.**</span>

위 우선순위를 주의해서 CSS를 작성하자.

---