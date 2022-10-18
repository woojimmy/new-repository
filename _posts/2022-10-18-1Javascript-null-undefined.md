---
title: "[Javascript] 기초 이론 - null과 undefined"
excerpt: "Javascript에서 등장하는 null과 undefine의 의미와 차이점을 알아보자."

categories: 
  - Javascript
tags: [Javascript, theory, wecode]
toc: true
author_profile: true 
sidebar:
   nav: "docs"
---

# null & undefined
Javascript에서는 '없음'을 나타내는 값이 두 가지가 있다. 하나는 `null`이고, 다른 하나는 `undefined`이다. 같은 의미를 가지지만 각각 사용되는 목적과 위치가 다르다.

## <span style="color:cornflowerblue">**undefined**</span>
`null`보다 `undefined`를 먼저 알아보는 것이 쉽다. <br> `undefined`는 Javascript에서 value(값)이 할당되지 않은 경우를 의미한다. 
```javascript
var example;
console.log(example)  //---undefined

let secondExample;
console.log(secondExample)  //---undefined
```
<img src="/assets/images/20221018/undefined.png"><br>

## <span style="color:cornflowerblue">**null**</span>
`null`은 **'빈 값(black)'**를 의미하는데, `undefined`와 차이점은 `null`은 사용자가 값이 없다는 것을 입력할 때 사용한다는 점이다.<br>
만약 빈 값에 `undefined`를 쓰면 어떻게 되는지 다음 코드를 입력해보자.
```javascript
let example; // value를 할당하지 않음
let secondExample = undefined;  // 'undefined'라는 value 할당

console.log(example); // ---undefined
console.log(secondExample); // ---undefied(?)
```
<img src="/assets/images/20221018/null1.png"><br>

여기서 밑의 `console.log(secondExample);`가 `undefined`라고 뜨는데, 이것이 할당이 되지 않은 것인지, `undefined`라는 value가 나타나는 것인지 알 수가 없다. 그렇기 때문에 사용자가 직접 '빈 값'을 입력하기 위해선 `null`을 쓰는 것이 더 바람직하다.
```javascript
let example; // value를 할당하지 않음
let secondExample = null;  // 'null'이라는 blank value를 할당

console.log(example); // ---undefined
console.log(secondExample); // ---null
```
<img src="/assets/images/20221018/null2.png"><br>

여기서 `null`과 `undefined`의 차이가 보인다. `console.log(secondExample);`에서 `null`이라는 값이 나온 것을 보면, `null`은 `undefined`처럼 value가 아예 정의되지 않은 것이 아니라, `null`자체가 **'value가 없다'라는 의미를 가진 value라는 것**이다. 만약 `null`이 `undefined`와 완전 동일하게 '값이 없음' 자체를 의미했다면 `console.log(secondExample)`에서 `undefined`가 출력되었어야 했다.

## <span style="color:cornflowerblue">**'엄격일치연산'과 'typeof'로 확인**</span>
아래 코드를 입력해보자
```javascript
let name;  // ---undefined
name = null;  //  ---null

console.log(null == undefined);  // ---true
console.log(null === undefined);  // ---false
```
<img src="/assets/images/20221018/truefalse.png"> <br>

왜 두 가지 console이 다른 결과가 나올까??<br> 그 이유는 위에서 **`==`는 단순히 'value'만 같다는 것을 의미하지만, `===(엄격일치연산)`은 'value'뿐만 아니라 'type' 또한 같아야 하기 때문** 이다. <br> 그렇다면 'type'은 어떻게 확인할까?? <br> Type 확인을 위해선 `typeof`라는 연산자를 사용하면 된다.
```javascript
console.log(typeof null);  //  ---object
console.log(typeof undefined);  //  ---undefined
```
<img src="/assets/images/20221018/typeof.png"><br> 
위처럼 `null`의 type은 `object`가 출력된다. 이렇게 type이 다르기 때문에 `===`을 사용했을 때 `false`가 출력되는 것이다.

---

