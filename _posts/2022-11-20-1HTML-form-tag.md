---
title: "[Javascript][HTML] - 페이지 이동 문제 해결 - <form>태그의 type='submit'"
excerpt: "Javascript에서 <form> 태그의 submit 이벤트로 인한 페이지 이동이 되지 않는 문제 해결하는 방법을 알아보자."

categories: 
  - HTML_CSS
tags: [HTML, Javascript, form, tag]
toc: true
author_profile: true 
sidebar:
   nav: "docs"
---

# [로그인 페이지 > 메인 페이지] 로그인 버튼 클릭으로 이동

## 문제점
instagram을 클론한 'westagram'이라는 사이트를 만드는 중이다. <br> 로그인 페이지와 메인(게시글) 페이지를 만든 후, 로그인 페이지에서 ID와 Pw input field에 조건에 충족하는 ID, Pw를 입력한 뒤에 로그인 버튼이 색이 바뀌며 활성화 <br> -> 버튼 클릭 시 로그인 페이지에서 메인 페이지로 이동. <br> 이러한 동작을 구현 중인데, 문제가 발생했다.
<img  src="/assets/images/20221120/Westagramloginvideo1.gif">
<br>

 로그인 버튼을 눌러도 새로운 페이지로 이동하지 않고 새로고침이 된다. <br>
로그인 버튼과 관련된 코드는 다음과 같다
```javascript
// 버튼 클릭 이벤트
loginBtnElement.addEventListener('click', function(e) {
  let loginInputIDField = loginInputId.value;
  let loginInputPWField = loginInputPw.value;

  const checkEMail = loginInputIDField.indexOf("@");

  if(loginInputIDField.length == 0) {
    // 아무런 text도 존재하지 않을 때
    alert('사용자 이메일을 입력해주세요.')  
  } else if(checkEMail == -1) {
    // 이메일에 `@`가 포함되지 않을 때
    alert('올바른 이메일을 입력해주세요.')  
  } else if(loginInputPWField.length == 0) {
    // 이메일에 `@`가 포함되지만 비밀번호에 아무것도 입력되지 않았을 때
    alert('비밀번호를 입력해주세요.')  
  } else if(loginInputPWField.length < 5) {
    // 이메일에 `@`가 포함되지만 비밀번호가 5자리 이하일 때
    alert('비밀번호는 5자 이상입니다. 다시 입력해주세요.')  
  } else {
    // 위 조건들을 모두 충족하여 메인 페이지로 이동하기
    loginToMainPage();  }  
})

// 메인 페이지(url)로 이동하는 함수
const loginToMainPage = () => {
  window.location.href = '/students/40th/woojin/main.html';
}

// loginBtnElement: 로그인 버튼 element
// loginInputId: 아이디 입력 input element
// loginInputPw: 비밀번호 입력 input element
```

## 무엇이 문제인가?
### url(?)
밑의 메인 페이지로 이동하는 함수 `loginToMainPage`에서 메인 페이지로 접근하는 url이 잘못되지 않았을까? 라고 처음 생각했었다.
그러나 `window.location.href`이 아닌, `window.open`으로 변경하면 잘 작동하기 때문에 url이 잘못되지 않았다는 것을 알 수 있다.
```javascript
const loginToMainPage = () => {
  // window.location.href = '/students/40th/woojin/main.html';
  window.open('/students/40th/woojin/main.html');
}
```
<img  src="/assets/images/20221120/Westagramloginvideo2_windowopen.gif"> <br>

새 탭으로는 연결이 매우 잘 된다. 즉, url의 문제는 아니라는 것. <br>
이 방법을 쓰면 편하겠지만 로그인 페이지는 새로고침되어 그대로 두고, 새 탭에서 메인 페이지로 넘어가는 것은 올바른 형식이 아니라 생각이 든다. <br> 
그렇기 때문에 현재 탭에서 url로 연결되는 방식을 사용하고 싶었다. <br>
그래서 `window.open` 대신 `window.location.href`를 사용했던 것인데... 결과는 위에서 말한대로...

### window.location.href(?)
그렇다면 `window.location.href`라는 접근 방식이 잘못된 것일까...? 사실 이것은 mdn과 같은 공식 문서를 참고했기에 잘못될 가능성이 낮다고 생각한다. <br>
그치만 어쩌겠는가 안되면 Test 해봐야지...! <br>
test를 위해 새로운 js 파일을 생성하고, 이번엔 메인페이지에서 로그인 페이지로 넘어가게 설정했다. <br>
로그인 페이지에서 문제가 되는 부분이 `<button>`이기 때문에 메인 페이지에서도 `<button>`인 좋아요와 보내기 버튼 사이의 댓글버튼에 다음과 같은 동작을 설정하였다.
```javascript
const commentBtnArticle = document.getElementById('commentBtmArticle')

commentBtnArticle.addEventListener('click', function(e) {
    loginToLoginPage();
})

const loginToLoginPage = () => {
    window.location.href ='/students/40th/woojin/login.html';
  } 
```
<img  src="/assets/images/20221120/Westagramloginvideo3_windowlocation.gif"> <br>
역시 제대로 작동한다. 그렇다면 url 접근 방식도 문제가 아니라는 뜻! <br>
그렇다면 도데체 뭐가 문제지.....

### eventListener(?)
그 다음... 슬슬 머리가 깨질 것 같다ㅎㅎ 그렇다면 내가 `click`에 대한 `addEventListener`를 잘못 설정한 것일까? <br>
`click` 이벤트에 `console.log`를 찍어보자. 다음과 같은 코드를 `addEventListener`의 제일 첫 번째에 추가했다.
```javascript
  console.log('click');
```
<img  src="/assets/images/20221120/Westagramloginvideo4_clickevent.gif"> <br>
음??????? <br>

분명 클릭 시 `click`이 찍힌다. 그러나 바로 사라진다. <br>
Console 창에 `Preserve log`부분을 활성화해서 다시 찍어보자
<img  src="/assets/images/20221120/Westagramloginvideo5_consolelog.gif"> <br>

제대로 찍히는 것을 보면 분명 `click` 이벤트는 정상적으로 작동한다. <br>
즉, `addEventListener`에도 문제가 없음을 알 수 있다.

### <form> 태그의 submit (!)
javascript의 모든 기능은 정상적으로 작동한다. 근데 왜!!! <br>
지금 문제는 페이지가 버튼을 클릭할 때마다 새로고침되는 것이다. 아마 클릭 후 메인 페이지로 넘어가기 전에 새로고침이 먼저 되서 그런것 같다. <br>
결국 멘토님의 도움을 받기로 했다. <br>
계속 시도해봤던 것들을 설명드리니 단번에 혹시 `<form>` 태그를 쓰지 않았냐고 물으신다 <br>
그렇다. Semantic tag를 여러 가지 사용해보기 위해, 그리고 instagram을 클론했기에 로그인 페이지의 input과 button을 `<form>`태그로 감쌌었다. <br>
문제는 내가 `<form>`태그에 완벽히 이해하지 못하고 사용했다는 것이다.
<br><br>
`<form>`태그는 `type`을 `submit`으로 default로 가지고 있다고 한다. 그렇기 때문에 `<form>`태그 안에 어떠한 이벤트를 설정하면 그대로 제출되어 reload 되는 현상이 발생한다. <br>
그러므로 이 `submit`을 제어하기 위한 방법을 사용해야 내가 겪었던 문제를 해결할 수 있었다. 이제 제어하는 방법을 알아보자.

## 해결 방법
우선 해결 방법은 2가지가 있다.
### 1. type="button"
첫 번째 방법은 `<form>`태그 안에 있는 `<button>`에게 별도로 `type="button"`을 추가해주는 것이다.<br>
`<button>`태그에는 기본적으로 attributes가 `button`, `reset`, `submit`이 있다.(`<button>`이라고 해서 무조건 `button` type을 가지지 않는다는 것을 유의하자) <br>
위에서 말한대로 `<form>`태그는 default로 `submit` type을 가지기 때문에 `<button>` 또한 `submit`을 default로 가져 우리가 원하는 동작을 위해서는 type을 바꿔줘야 한다.<br>
그러므로 html 파일에서 로그인 버튼에 `type="button"`을 추가해준다면 정상적으로 메인 페이지로 넘어가게 된다.
```html
<button type="button" id="loginBtn">로그인</button>
```


### 2. Event.preventDefault
두 번째 방법은 Javascript에서 `click` 이벤트 시 `Event.preventDefault()`를 입력하는 것이다.<br>
`Event.preventDefault()`는 주로 html에서 `<a>`태그나 `<submit>`과 같이 고유의 동작을 block하는 역할을 한다.
즉, 내가 설정한 `click` 이벤트에 `Event.preventDefault()`를 삽입하면, `<form>`태그로 인해 발생하는 `submit`이 동작하지 않게 되고,<br>
동작이 무시된 채로 코드가 진행되어 `loginToMainPage`라는 함수에 도달할 수 있는 것이다. <br>
선택적으로 동작을 무시할 수 있다는 점이 알아두면 유용할 것이란 생각이 든다.
```javascript
loginBtnElement.addEventListener('click', function(e) {
  e.preventDefault();  /// 추가한 코드!!!!!!!!!!!!!!
  let loginInputIDField = loginInputId.value;
  let loginInputPWField = loginInputPw.value;

  const checkEMail = loginInputIDField.indexOf("@");
  if(loginInputIDField.length == 0) {
    alert('사용자 이메일을 입력해주세요.')
  } else if(checkEMail == -1) {
    alert('올바른 이메일을 입력해주세요.')
  } else if(loginInputPWField.length == 0) {
    alert('비밀번호를 입력해주세요.')
  } else if(loginInputPWField.length < 5) {
    alert('비밀번호는 5자 이상입니다. 다시 입력해주세요.')
  } else {
    loginToMainPage();  }
})

const loginToMainPage = () => {
  window.location.href = '/students/40th/woojin/main.html';  
}
```
<img  src="/assets/images/20221120/Westagramloginvideo6_success.gif"> <br>
위 두 방법 모두 성공적으로 작동하는 것을 확인했다!!

