---
title: "[Javascript] 기초 이론 - 데이터 타입(Data Type) - 숫자와 문자열(String)"
excerpt: "Javascript에서 Data type 중 '숫자 타입'과 '문자열(String)'에 대해 알아보자."

categories: 
  - Javascript
tags: [Javascript, theory, datatype]
toc: true
author_profile: true 
sidebar:
   nav: "docs"
---

# 데이터 타입(Data type)

## <span style="color:cornflowerblue">**숫자 타입**</span>
Javascript에서는 정수, 실수, 음의 정수, 2진수, 8진수, 15진수 등을 data type으로 할 수 있다. <br>
```javascript
let example = 10;  //  정수
let secondExample = 10.15;  //  실수
let thirdExample = -20;  //  음의 정수
```
2진수, 8진수, 16진수 리터럴은 이들의 값을 참조하면 모두 10진수로 해석된다.
```javascript
let binary = 0b01000001;  //  2진수
let octal = 0o101;  // 8진수
let hex = 0x41;  //  16진수

console.log(binary);  //  ---65
console.log(octal);  //  ---65
console.log(hex);  // ---65
console.log(binary === octal);  //  ---true
console.log(octal === hex);  //  ---true
```
<img src="/assets/images/20221019/numberdatatype.png"> <br>
위 코드는 모두 `65`라는 value를 각각 2진수, 8진수, 16진수 리터럴로 나타낸 것이며, value와 type이 각각 `65`와 `숫자 타입`으로 동일하기 때문에 엄격일치연산(`===`)에서 `true`가 출력된다. <br> 사실 Javascript는 정수만을 위한 data type이 존재하지 않고, 모든 수를 **실수**로 처리한다.

```javascript
console.log(1 === 1.0);   //  ---true

console.log(4 / 2);  //  ---2
console.log(3 / 2);  //  ---1.5
```
그렇기 때문에 제일 첫 코드에서 `true`가 출력되고, '정수'끼리 나누기를 실행해도 '실수'로 출력되는 것을 알 수 있다. <br><br> 숫자 타입은 추가적으로 세 가지 특별한 value도 표현할 수 있다.
```javascript
console.log (10 / 0);  //  ---Infinity
console.log(10 / -0);  //  ---(-Infinity)
console.log(1 * 'String');  //  ---NaN
```
<img src="/assets/images/20221019/numberinfinity.png"><br>
- Infinity: 양의 무한대
- -Infinity: 음의 무한대
- NaN: 연산 불가 (Not-a-Number)

`NaN`은 Javascript가 대소문자를 구분하기 때문에 주의해야한다. `nan`, `Nan`과 같이 대소문자가 다르면 value가 아닌 식별자로 해석하기 때문이다.
```javascript
let example = NaN; //  ---undefined
let secExample = naN;  //  ---ReferenceError: naN is not defined
let trdExample = Nan;  //  ---ReferenceError: Nan is not defined
```
<img src="/assets/images/20221019/numbernan.png"><br>

## <span style="color:cornflowerblue">**문자열(String)**</span>
문자열(String)은 텍스트 데이터를 나타내는 데 사용한다. <br> 작은 따옴표(`' '`), 큰 따옴표(`" "`), 백틱으로 텍스트를 감싼다.
```javascript
let string = `작은 따옴표`;
let string2 = "큰 따옴표";
let string3 = `백틱`;

let string4 = '작은 따옴표로 감싼 문자열의 "큰 따옴표"는 문자열로 인식';
let string5 = "큰 따옴표로 감싼 문자열의 '작은 따옴표'는 문자열로 인식";
```
만약 이러한 따옴표나 백틱으로 감싸지 않는다면, javascript 엔진은 식별자나 키워드로 인식하고, 띄어쓰기를 포함할 수 없다.

## <span style="color:cornflowerblue">**숫자 타입, 문자열(String) 연산**</span>

문자열의 연산 중 사이에 '띄어쓰기'를 삽입하고 싶다면 `' '`를 입력하면 된다. 작은 따옴표(`' '`)사이에는 공백이다.
```javascript
let naMe = 'Woojin' + 'Lim';
let namE = 'Woojin'+' '+'Lim';

console.log(naMe);  //  ---WoojinLim
console.log(namE);  //  ---Woojin Lim
```
<img src="/assets/images/20221019/stringplusstring.png"><br>

다음은 헷갈릴 수 있는 코드를 예시로 정리해봤다.
```javascript
console.log(2 + 2);  //  ---4 (숫자 + 숫자)

console.log('2'+'2');  //  ---22 (문자열 + 문자열)

console.log(2 + '2');  //  ---22 (숫자 + 문자열)

console.log(3 + 2 + '2');  //  ---52 (숫자 + 숫자 + 문자열)

console.log(2 + '2' + 2);  //  ---222 (숫자 + 문자열 + 숫자)
```
<img src="/assets/images/20221019/pluslist.png"><br>
숫자와 문자열을 구분하는 것이 중요함을 알 수 있다.