---
title: "[Javascript] - 객체 입력 오류 (Uncaught SyntaxError: Unexpected token ':')"
excerpt: "매우 기초적이고 부끄러운 객체 오류 해결"

categories: 
  - Javascript
tags: [javascript, object, error]
toc: true
author_profile: true 
sidebar:
   nav: "docs"
---
> 이번 글은 부끄러운 글일 수도 있지만, 다음에 같은 실수를 반복하지 않기 위해 적어본다..

# 객체 입력에서 오류가..?
## Uncaught SyntaxError: Unexpected token ':'
<img src="/assets/images/20221021/objecterror1.png"><br>
객체(Object)에 대한 강의를 들으면서 열심히 따라치고 있었는데 오류가 발생했다. 왜지..? <br> 처음엔 'token `:`'라 되어 있어서 `:`중 세미콜론(`;`)으로 잘못 
입력했나 싶어 다시 훑어봤지만 잘못된 점을 못찾았다. <br> 결국 구글링을 했고 결과는...

### 해결
객체 입력에서 **오타**가 있을 경우 발생하는 에러였다. 문자열이 제대로 `' '` 또는 `" "`로 감싸졌는지, `,`의 위치와 `()`, `{}`의  열림, 닫힘이 잘못된 부분이 있을 경우 해당 에러가 발생한단다.<br>
<img src="/assets/images/20221021/objecterror2.png"><br> 그렇다. 나는 눈뜬 장님이었다. `,`를 `.`으로 찍은걸 발견 못하다니...<br>

<img src="/assets/images/20221021/objecterror3.png"><br>
이제 알았으니 다음엔 구글링해서 시간쓰지 말고 바로 고칠 수 있게 기억해둬야겠다.

## Uncaught SyntaxError: Invalid shorthand property initializer
이번에 검색하는 김에 객체 입력에서 발생할 수 있는 비슷한 오류가 있나 찾아봤다. 그렇게 알게된 오류가 <br>`Uncaught SyntaxError: Invalid shorthand property initializer`!!<br>
<img src="/assets/images/20221021/objecterror4.png"><br>

### 해결
이 오류가 발생하는 이유는 객체 입력에서 `:`가 아닌 `=`를 사용했을 때 발생한다고 한다.<br>위 사진에서 `location`이 있는 한 줄만 `=`로 바꿨는데 바로 오류가 뜬다.<br> 아직은 긴 코드를 Javscript로 작성해본적이 없어서 이런 실수는 잘 안할거 같은데, 혹시 모르니 알아는 둬야겠다.

## 개발자 도구로 오류 위치 찾기
나는 JS bin으로 처음 입력해보는 객체를 연습하다보니 에러가 발생했을 때 구글링을 했는데, 해결하고나서 생각해보니까 브라우저에 개발자도구를 이용하면 에러 이유와 위치를 쉽게 알 수 있을거라는 생각이 들었다...<br>
제일 처음 오류가 발생한 코드를 브라우저의 `console`창에 입력해보자.
<img src="/assets/images/20221021/objecterror5.png"><br> 아까처럼 에러가 뜬다. 여기서 빨간색의 에러줄 오른쪽에 `VM401:6`이라는 글씨를 클릭하면 `source`창에서 에러 발생 위치를 추적할 수 있다.
<img src="/assets/images/20221021/objecterror6.png"><br> 정말 친절하다. <br> 찾다보니 나중에 직접 웹 페이지를 만들고 디버깅할 때 개발자도구를 많이 사용하는거 같다. 지금부터라도 개발자도구를 사용하는 버릇을 들여야겠다.