---
title: "[HTML] 기초 이론 - HTML의 Tags"
excerpt: " HTML의 구조와 많이 쓰이는 Tag들에 대해 알아보자 - wecode 사전스터디."

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

# HTML 태그(Tag)
## <span style="color:cornflowerblue">**HTML 필수 Tag와 구조 파악**</span>
HTML의 파일은 다음과 같은 구조를 가진다.
```html
<!DOCTYPE>
<html>
    <head>
        <body>
        </body>
    </head>
</html>
```
위 코드의 tag들을 하나하나 살펴보자
### <span style="color:cornflowerblue">**`<!DOCTYPE>`**</span>
`<!DOCTYPE>`은 HTML파일에서 가장 첫 줄에 위치해야 하는 '선언문'입니다. **모습은 tag와 비슷하지만 HTML tag는 아니다.**  `<!DOCTYPE>`은 이 HTML파일이 어떠한 버전의 HTML을 이용했는지 부라우저에 알려주는 역할을 한다. 
```html
<!DOCTYPE html>
```
이 선언문은 HTML5 버전을 사용한다는 의미이다. 가장 최신 버전이기 때문에 가장 많이 쓰이고 있다.

---

### <span style="color:cornflowerblue">**`<html>`**</span>
`<!DOCTYPE>`를 제외하고 모든 HTML elements들은 `<html></html>` tag로 감싸져 있다. 브라우저가 `<html>` tag를 만나면, HTML이 시작됐는지 인지하고 elements를 그릴 준비를 한다.

---

### <span style="color:cornflowerblue">**`<head>`**</span>
```html
<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width">
    <title>repl.it</title>
</head>
```
`<html>` tag 다음에는 항상 `<head>` tag가 위치한다. 이 tag 안에는 사이트의 제목, 설명, 부가 정보, 기술적 내용이 들어가는 부분이다. `<head></head>`로 감싸진 위 코드를 한 줄씩 살펴보자.

- **`<meta charset="utf-8">`**<br>: 한글, 일본어, 중국어가 포함된 page라면 '**utf-8**'이라는 값으로 문자 인코딩을 추가해줘야 한다.

- **`<meta name="viewport" content="width=device-width">`**<br>: 디바이스(device)의 가로 크기가 곧 웹 페이지의 가로 크기와 같다는 의미이다. 이 정보를 추가하지 않는다면 데스크탑 버전의 웹 페이지가 축소되어 보이는 현상이 나타난다.
- **`<title>repl.it</title>`**<br> : 브라우저 탭에 보이는 페이지 이름이다. 여기선 'repl.it'이 페이지 이름이 된다.

---

### <span style="color:cornflowerblue">**`<body>`**</span>
`<body>` tag는 항상 `<head>` tag 다음에 위친한다. `<body>` tag 내부에 위치한 tag들은 브라우저 화면에 보여질 tag들이다.

---
## <span style="color:cornflowerblue">**HTML의 Tag**</span>
HTML 파일에서 자주 쓰이는 tag들을 알아보자.
### <span style="color:cornflowerblue">**`<h1>` ~ `<h6>`**</span>
- 주로 브라우저에서 제목같은 강조된 텍스트를 보여줄 때 사용된다.
- 1에서 6으로 갈수록 크기가 작아진다.
- **`<h1>`** tag는 한 페이지에서 단 한번만 사용되어야 한다.
- **`<h2> ~ <h6>`** tag는 한 페이지에 여러번 사용이 가능하다.
- **`<h1> ~ <h6>`** tag는 순차적으로 사용해야 한다.<br>(`<h3>` tag를 사용하려면 그 전에 `<h1>, <h2>` tag가 존재해야 한다.)
- `<h>`는 **heading**의 줄임말이다.
- 예시↓

```html
<h1>목차</h1>
<h2>중요한 태그들</h2>
<h3>heading</h3>
```

---

### <span style="color:cornflowerblue">**`<a>`**</span>
- `<a>` tag는 링크를 걸어주는 tag이다.
- `<a>` tag에 `href`라는 속성(attribute)에 링크할 주소를 입력한다.
- `target`이라는 attribute에 **"_blank"** 값을 입력하면 링크 연결시 새로운 탭에서 주소가 열리게 해준다.
- `target="_blank"`가 없으면 현재 탭에서 열리게 된다.
- `<h>`는 **anchor**의 줄임말이다.
- 예시↓
  
```html
<a href="https://woojimmy.github.io/" target="_blank">블로그 이동</a>
```

---
### <span style="color:cornflowerblue">**`<p>`**</span>
- `<p>` tag는 텍스트를 주로 넣는다.
- `<p>` tag는 **paragraph**의 줄임말로, 문단을 통으로 넣을 때가 많다.
- `<p>` tag는 `<span>` tag와 달리 줄바꿈이 발생한다.
- 예시↓
  
```html
<p>tag 파헤치기</p>
<p>문단, paragraph</p>
```

---
### <span style="color:cornflowerblue">**`<span>`**</span>
- `<span>`tag에는 `<p>` tag처럼 텍스트를 주로 넣는다.
- `<span>` tag는 줄바뀜이 발생하지 않는다.
- 이렇게 한 줄에 이어서 나오는 element를 **inline-element**라고 한다.
- 예시↓

```html
<span>이름: Woojin</span>
<span>직업: null</span>
```

---
### <span style="color:cornflowerblue">**`<div>`**
- `<div>` tag는 **division**의 줄임말
- 웹 사이트의 섹션을 나눌 때 사용한다.
- `<div>` tag는 아무런 의미를 가지고 있지 않는다.
- 예시↓

```html
<div>
    HTML의 Tag
</div>
```

---

<br><br>
<br>
>HTML에는 많은 tag가 있지만, 가장 많이 쓰이는 tag 몇가지를 알아봤다. 다음엔 HTML의 속성(attribute)들에 대해 알아보자.