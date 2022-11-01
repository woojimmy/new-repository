---
title: "[Javascript] - 문자열 심화 - Text찾기, 변환하기"
excerpt: "Javascript의 문자열에서 특정 text를 찾고 변환하는 코드를 살펴보자."

categories: 
  - Javascript
tags: [Javascript, theory, string]
toc: true
author_profile: true 
sidebar:
   nav: "docs"
---

# 문자열
오늘의 예시 코드이다.
```javascript
const info = "JavaScript는 프로래밍 언어이다.";
const firstChar = info.indexOf("프로래밍"); 

console.log(firstChar);

if (firstChar !== -1) { 
  info = info.slice(0, firstChar) + "프로그래밍" + info.slice(firstChar+4, info.length); 
}

console.log(info);
```
(console에 입력시 오류가 나는 것은 정상! 오류가 나는 원인은 조금 이따 살펴보자)

## 문자열에서 Text 위치 찾기
```javascript
const info = "JavaScript는 프로래밍 언어이다.";
const firstChar = info.indexOf("프로래밍"); 

console.log(firstChar); // ---12
```
- 문자열의 값을 가지는 `info`라는 변수를 선언했다.
- `firstChar`는 `info`의 값에서 특정 text를 찾아주는 변수이다. <br>`대상변수.indexOf(찾을 text);` → index`O`f이다. 대문자 주의!
- 위 코드에서 `프로래밍`은 문자열의 12번째 위치에서 등장한다. 그러므로 `console.log`에서 `12`가 출력! (첫 글자는 `0`이다!)

그렇다면 만약 찾을 text가 변수의 문자열에 없으면 어떻게 나올까?? <br> `0`은 문자열의 첫 번째를 의미하기 때문에 `0`이 오면 안되는데 뭐라 나올지 궁금하니 쳐보자
```javascript
const info = "JavaScript는 프로래밍 언어이다.";
const firstChar = info.indexOf("자바스크립트"); 

console.log(firstChar); // ---(-1)
```
`-1`이 출력된다!! 그렇기 때문에 예시 코드의 `if` 부분에서 조건을 보면 `firstChar !== -1`인 것은 `firstChar`이 `-1`이 아닐 때. 즉, `firstChar`에서 찾고자하는 text가 대상하는 변수에 존재할 때 이 조건이 충족되어 `if`가 실행된다는 것을 알 수 있다! <br><br> 한 가지 더 궁금한게 생겼다. 그럼 찾고 싶은 text가 복수일 때는??
```javascript
const info = "JavaScript 언어는 프로래밍 언어이고 언어이며 언어이다.";
const firstChar = info.indexOf("언어"); 

console.log(firstChar); // ---11
```
결과는 가장 앞에 있는 `언어`의 위치만을 찾아준다.
### 가장 앞 말고 다른 text 위치 찾기
만약 문자열에 찾고 싶은 text가 여러개라면 그 위치들을 알 방법은 없을까?? 당근 있다.
```javascript
const info = "JavaScript 언어는 프로래밍 언어이고 언어이며 언어이다.";
const firstChar = info.indexOf("언어", 12); 

console.log(firstChar); // ---20
```
`firstChar`변수 선언문에서 `index()`의 괄호(`( )`)안에 `(찾을 text, position)`을 입력하면 입력한 `position`에서부터 해당 text를 찾아 위치를 알려준다. 직접 해보니 `position` 앞에 있는 text는 제외하지만, 위치를 나타낼 때는 전체 문자열을 기준으로 하는것 같다. <br><br>