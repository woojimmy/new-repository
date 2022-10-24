---
title: "[Javascript] - 헷갈리는 표현식 - 'num++'"
excerpt: "Javascript에서 표현식 중 헷갈리는 'num++'에 대해 정리해보자."

categories: 
  - Javascript
tags: [Javascript, theory, expression]
toc: true
author_profile: true 
sidebar:
   nav: "docs"
---

# num++

## 무엇이 헷갈리는가?
> `num++`는 `num = num + 1`과 동일한 의미이다.

```javascript
let num = 1;
let newNum = num++;

console.log(num);   //  ---2
console.log(newNum);   //  ---1
```
<img src="/assets/images/20221024/expression1.png"> <br> 여기서
-  `console.log(num);`에서 `2`가 출력되는 것
-  `console.log(newNum);`이 `1`이 출력되는 것 

모두 이해가 되지 않았다. <br><br> 우선 첫 번째 줄에서는 `num`이라는 변수의 값은 `1`이고, 그 밑에 `num`의 값이 변할 부분이 없다고 생각했기 때문에 `console.log(num);`가 `1`이 출력될 것이라 예상했는데 `2`가 출력되었다. <br> 그리고 `console.log(newNum);`은 `num++`이라는 값. 즉, `num + 1`이기 때문에 `2`가 출력될 것이라 생각했다.
```javascript
let num = 1;
num++;
console.log(num);
```
<img src="/assets/images/20221024/expression2.png"> <br>
이렇게 밑에 선언문 밑에 `num++`라는 표현식이 있었다면 `console.log(num);`에서 `2`가 출력되어도 이해가 되지만, 내가 헷갈려했던 코드에서는 밑에 `newNum`이라는 변수를 선언하는 선언문이 있다. 이것은 선언문이기 때문에 `num`의 값이 변하지 않을 것이라 생각했는데 이것은 내가 잘못 생각한 것이다.

## 이해하기
```javascript
let newNum = num++;
```
가장 중요한 부분은 여기다. 이 선언문은 2단계의 과정으로 진행된다. <br> (마치 `let abc = 1;`이라는 코드에서 '선언 → 할당' 처럼 동시에 한 줄의 코드가 진행되는 것이 아닌 단계적인 과정을 말한다.) <br> **코드의 진행은 앞에서부터 순차적으로 진행하는 점을 기억하자.** 그렇다면 2단계의 과정은 다음과 같다.
```javascript
let newNum = num  //   ----- 1 Step
num++  //   ----- 2 Step
```
1. `newNum`이라는 변수명이 선언되고, `num`이라는 값이 할당된다.
2. `num`이라는 값에 `1`이 더해진다.

이것을 제일 위 문제의 코드에 대입해보면
```javascript
let num = 1;  //  ----- `num`은 `1`이다.
let newNum = num;  //  ----- 'newNum`은 `num`이고, `num`은 `1`이므로 `newNum`은 `1`이다.
num++;  //   ----- `num`에 1을 더하므로 `2`가 된다.

console.log(num);   //  ---2
console.log(newNum);   //  ---1
```
`newNum`은 `num`에 `1`을 더하기 전에 변수가 선언된다. 그렇기 때문에 `console.log(newNum);`이 `1`이 출력되는 것이다. <br> 그러나 `num`은 마지막에 `num++`에 의해 `1`이 추가되므로 모든 코드가 진행된 후에는 `num = 2`가 된다. 그러므로 `console.log(num);`이 `2`가 출력되는 것이다. <br>어려울 때는 쉽게 이해하기 위해 이렇게 풀어서 적어봐야겠다.

## 응용하기
만약 `console.log(newNum);`이 `2`를 출력하기 위해선 어떻게 해야할까? <br>
console.log로 출력되기 전에 `num++`가 있어야 한다. 즉, `let newNum = num;`선언문 전에 `num++`가 있어서 `num`이 `2`라는 값을 가져야한다. 그러므로 다음과 같이 코드를 변경할 수 있겠다.
```javascript
let num = 1;
num++;
let newNum = num;

console.log(num);   //  ---2
console.log(newNum);   //  ---2
```
<img src="/assets/images/20221024/expression3.png"> <br>

이렇게하면 `console.log(newNum);`에서 `2`가 출력된다!
```javascript
num++;
let newNum = num;
```
다음에는 이 코드를 처음처럼 1줄로 줄이는 방법을 생각해보자. 코드는 앞에서부터 순차적으로 진행되므로 `num++`가 먼저 나오면 될텐데 어떻게 입력해야 할까?
```javascript
let newNum = ++num;
```
바로 이렇게 `++`를 `num` 앞에 쓰면 된다. 이러면 `++`가 먼저 진행되고 변경된 `num`으로 `newNum` 변수가 선언된다! <br> 줄인 코드를 위 `console.log(newNum);`이 있는 코드에 적용해보면
```javascript
let num = 1;
let newNum = ++num;

console.log(num);
console.log(newNum);
```
<img src="/assets/images/20221024/expression4.png"> <br> 적상적으로 작동한다!!

