---
title: "[Javascript] 기초 이론 - 표현식(Expression)과 문(Statement)"
excerpt: "Javascript에서 표현식(expression)과 문(statement)의 의미와 예시를 알아보자."

categories: 
  - Javascript
tags: [Javascript, theory, expression, statement]
toc: true
author_profile: true 
sidebar:
   nav: "docs"
---

# 표현식(Expression)과 문(Statement)

## <span style="color:cornflowerblue">**값(Value)**</span>
값(Value)은 코드에 있는 식이 평가(Evaluate)되어 생성된 결과를 말한다.
- 평가(Evaluate): 식을 해석해서 값을 생성하거나, 참조하는 것을 의미.

```javascript
10 + 20; // ---30
```
<img src="/assets/images/20221018/valuetheory.png"> <br> 위 코드는 `10 + 20`이라는 식이 evaluate되어 `30`이라는 value를 생성한 것이다.

```javascript
let sum = 10 + 20;
sum; // ---30
```
즉, 위 코드에서 선언된 `sum`이라는 변수에 할당된 value는 `10 + 20`이 아닌 `30`이라는 것을 의미한다. <br> Value는 다양한 방법으로 생성할 수 있지만 가장 기본적으로 '리터럴(literal)'을 사용한다.

---
## <span style="color:cornflowerblue">**리터럴(Literal)**</span>
리터럴(Literal)은 **사람이 이해할 수 있는 문자 또는 약속된 기호를 사용해 value를 생성하는 표기법**이다. <br> Literal의 종류는 다음과 같다.

|리터럴(Literal)| <center>예시</center> | <center>비고</center>
|:---:|:----|:-----|
정수 리터럴|100| |
부동소수점 리터럴| 10.5| |
2진수 리터럴| 0b0100001| 0b로 시작 |
8진수 리터럴 | 0o101 | ES6에서 도입, 0o로 시작 |
16진수 리터럴 | 0x41 | ES6에서 도입, 0x로 시작 |
문자열 리터럴 | 'Hello' <br> "World" | |
불리언 리터럴 | true <br> false | |
null 리터럴 | null |
undefined 리터럴 | undefined |
객체 리터럴 | { name: 'Woojin', address: 'Seoul' } | 
배열 리터럴 | [1, 2, 3] | 
함수 리터럴 | function() {} |
정규 표현식 리터럴 | /[A-Z]+/g |

---
## <span style="color:cornflowerblue">**표현식(Expression)**</span>
표현식(Expression)은 value로 평가 될 수 있는 문(Statement)이다.
```javascript
let myScore = 100;  // ---100
```
위 코드에서 `100`은 '정수 literal'이다. 이 `100`이라는 '정수 literal'은 Javascript 엔진에 의해 평가되어 `100`이라는 value를 생성한다. <br> 그러므로, `100` 자체로 **표현식(expression)**이 된다.

```javascript
let myScore = 50 + 50;  // ---100
```
여기서는 `50`인 '정수 literal'과 `+`라는 '연산자'로 이루어져 있다. 여기도 마찬가지로 `50 + 50`이라는 '정수 literal'과 '연산자'가 평가되어 `100`이라는 value를 생성하므로 `50 + 50`이 **expression**이 된다.
```javascript
myScore; //  ---100
```
만약 위 코드들처럼 `myScore`라는 변수를 선언하고, 이 식별자를 참조해보자. 그러면 `myScore`라는 식별자가 `100`이라는 value로 평가된다. 비록 식별자 참조는 value를 생성하지 않지만, value로 평가되므로 이러한 식별자(변수, 함수 등) 역시 **expression**이다. <br> Expression의 예시를 다음과 같이 정리해보았다.

```javascript
// 리터럴 only
100
'Hell0 World'

// 식별자 (선언이 이미 존재한다고 가정하자)
sum
person.name
arr[1]

// 연산자 포함
10 + 20
sum = 10
sum !== 10

// 함수, 메서드 호출 (선언이 이미 존재한다고 가정하자)
square()
person.name()
```
 ---
### 표현식의 동치(Equivalent)
표현식(Expression)은 값(Value)로 평가되므로, expression과 value는 동등한 관계인 **'동치(equivalent)'**이다. <br> 동치는 수학 수식을 예롤 들면, '1+2=3'이라는 식에서 `1+2`와 `3`은 같으므로 '동치'이다. <br> 따라서 expression과 value는 동등하므로 expression을 value의 자리에 작성할 수 있다는 것을 의미한다.
```javascript
let example = 1 + 2;

example + 3;  //  ---6
```
<img src="/assets/images/20221018/equivalent.png"> <br> 위 코드에서 `example + 3`은 표현식(expression)이다. 원래 `+`연산자는 좌항과 우항을 더하는 것이기에 각 항에 숫자가 존재해야 한다. 여기서 `example`은 첫 번째 줄에서 선언된 식별자, 즉 '식별자 표현식'이다. 그러므로 식별자의 value인 `3`대시 `example`이라는 '식별자 표현식'을 사용할 수 있다는 것을 의미한다. 이처럼 표현식은 다른 표현식의 일부가 되어 새로운 value를 만들어낼 수 있다.

---
## <span style="color:cornflowerblue">**문(Statement)**</span>
**문(Statement)은 프로그램(Program)을 구성하는 기본 단위, 최소 실행 단위를 의미한다.** Statement의 집합이 Program이며, Statement를 작성하고 순서에 맞게 나열하는 것이 Programming이다. <br>
Statement는 여러 '토큰(Token)'으로 구성된다.(Token은 아래에서 다시 알아보자.) <br> '문'은 컴퓨터에 내리는 명령어로 '명령문'이라고도 부른다. <br> 또한, 문은 실행하는 역할에 따라 '선언문', '할당문', '조건문', '반복문' 등으로 구분할 수 있다. 다음 코드들로 각 문별 예시를 살펴보자.
```javascript
//변수 선언문
let example;
var X;

//함수 선언문
function studentName () {}

//할당문
example = 100;
X = 'Hello';

//조건문
if (X > 1) {console.log(X);}

//반복문
for (var i = 0; i < 2; i++) {console.log(i);}
```

### 토큰(Token)
토큰(Token)은 **문법적으로 더 이상 나눌 수 없는 코드의 기본요소**를 말한다.<br> 예를 들어, 키워드, 식별자, 연산자, 리터럴, 세미콜론(`;`) 등등이 각각 문법적인 의미를 가지며, 더 이상 나눌 수 없는 기본 요소이므로 모두 **토큰(Token)**이다.
```javascript
let sum = 10 + 20;
// Token: let, sum, =, 10, +, 20, ;
```
---
## <span style="color:cornflowerblue">**표현식인 문, 표현식이 아닌 문**</span>
표현식(Expression)은 문(Statement)의 일부일 수도 있고, 그 자체로 statement가 될 수도 있다.
```javascript
let myScore; // 변수 선언문: 값이 평가되지 않는다 → 표현식이 아니다.

myScore = 20 + 50; // 할당문: 표현식이면서 완전한 문이다.
```
만약 표현식(expression)이 아닌 문(statement)을 변수에 할당하면 어떻게 될까??
```javascript
let example = var myScore;
console.log(example);
```
<img src="/assets/images/20221018/expression.png"> <br>
위 코드의 변수 선언문은 **'표현식이 아닌 문'**이다. 따라서, 변수 선언문은 value처럼 사용할 수 없다.

```javascript
let example = myScore = 20 + 50;
console.log(example);  // ---50
```
<img src="/assets/images/20221018/expression2.png"> <br>
할당문은 위에서 언급했듯 value를 평가할 수 있으므로 표현식(expression)이면서 완전한 문(statement)이다. 그렇기 때문에 value처럼 사용할 수 있고, 위 코드에서 `example`이라는 변수에 `70`이 할당되는 것을 볼 수 있다.




> 참고문헌: 모던 자바스크립트 Deep Dive - 이웅모 지음
