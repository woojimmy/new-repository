---
title: "[Javascript] 기초 이론 - 변수 네이밍(Variable Naming) "
excerpt: "Javascript에서 변수 이름은 어떠한 규칙을 가지고 있는지 알아보자."

categories: 
  - Javascript
tags: [Javascript, theory, variable]
toc: true
author_profile: true 
sidebar:
   nav: "docs"
---

# **변수** 네이밍(Variable Naming)
> 이번 글에선 변수의 이름을 짓는 규칙을 알아보자. 규칙에 위배되는 네이밍을 직접 Javascript에 입력해서 에러가 발생하는지 확인해보자.

## <span style="color:cornflowerblue">**변수**</span>의 네이밍 규칙
변수 이름(식별자, identifier)은 다음과 같은 네이밍 규칙을 가진다.
- Javascript에 사용되고 있는 '**예약어**'들은 식별자로 이용할 수 없다.
- 식별자는 **숫자**, **언더스코어(_)**, **달러 기호($)** 를 사용할 수 있으며, 이외의 특수문자는 사용할 수 없다.
- 단, 식별자는 언더스코어(_), 달러 기호($)로 시작할 수 있으나 **숫자로 시작하는 것은 허용되지 않는다**.

---

### <span style="color:cornflowerblue">**예약어(Reserved Word)**</span>
Javascript에서 지정된 예약어는 다음과 같다.<br>

| |  |  |   **예약어** |  |  |  |
|:-----:|:---:|:---:|:---:|:---:|:---:|:---:|
| await | break | case | catch | class | const | continue | 
| debugger | default | delete | do | else | enum | export 
| extends | false | finally | for | function | if | import |
| in | instanceof | new | null | return | super | switch |
| this | throw | true | try | typeof | var | void |
| while | with |

위의 이름들은 식별자로 선언해보자.<br><br>
<img src="/assets/images/20221006naming/reservedwordexample.png"><br>
이처럼 에러가 발생하면서 변수로 선언되지 않는다. 이는 이미 이 예약어들이 각자 정해진 동작이 정해져있기 때문이다.

이것 외에 식별자로 사용이 가능하지만, Javascript의 '엄격 모드(strict mode)'에서는 사용하지 못하는 예약어가 있다. 그것들은 다음과 같다.<br>
<span style="color:darkgrey">*(엄격 모드에 대해서는 더 공부해서 정리해야겠다...)*<span>

| |  |  |  |  |  |  |
|:-----:|:---:|:---:|:---:|:---:|:---:|:---:|
| implements | interface | let | package | private | protected | public | 
| static | yield |

----

### <span style="color:cornflowerblue">**특수문자 규칙**</span>
#### 식별자에 적용 가능한 특수문자
위 규칙처럼 **숫자**, **언더스코어(_)**, **달러 기호($)**는 식별자 이름에 사용 가능하다. 또한 **쉼표(,)**로 구분하면 하나의 문에서 여러 개를 선언할 수 있다.<br>
<span style="color:lightpink">*(하지만 가독성이 떨어지므로 권장되지 않는다.)*</span>
```javascript
var example$;
var example12345;
var ex_ample;
var example, woo_jin, Jim$$my;
```
<br><img src="/assets/images/20221006naming/undefined.png"><br>
이처럼 모두 'undefined'이 출력되면서 정상적으로 선언되었다.
<br>

----

#### 식별자에 적용 불가능한 특수문자
 위 규칙에서 한 가지 주의해야할 점이 있다. 바로 **언더스코어(_)**, **달러 기호($)**는 식별자의 처음에 올 수 있지만, **숫자**는 불가능하다.
 ```javascript
 var 2example;
 var _example;
 var $example;
 ```
 <img src="/assets/images/20221006naming/error1.png"><br>

또한, 위에서 언급한 기호 외의 특수문자를 사용하면 네이밍 규칙 위반으로 식별자로 사용할 수 없다.
```javascript
var ex-ample;
var example@@;
var ==example;
```
<img src="/assets/images/20221006naming/error2.png"><br>

---

#### 대문자와 소문자
Javascript는 대문자와 소문자를 구별한다. 그러므로 대소문자를 잘못 입력하지 않도록 주의해야한다. 만약 다르게 입력했다면 각각 별개의 변수로 선언되기 때문이다.
```javascript
var EXAMPLE = 50;
var example = 100;
var Example = 200;
var examPLE = 500;
```
<img src="/assets/images/20221006naming/capital.png"><br>
이처럼 같은 글자이지만 대소문자의 차이로 각각의 변수로 지정된 것을 확인할 수 있다.

---
#### 언어
식별자는 기본적으로 '유니코드 문자'를 허용하므로 한글, 일본어 등을 식별자로 지정할 수는 있다. 그러나 이는 권장되지 않는다.
```javascript
var 예시;
var こんにちは;
```
<img src="/assets/images/20221006naming/language.png"><br>
정상적으로 작동은 한지만... 알파벳을 쓰자!! 작동된다는 것을 알고만 있자

----

## 변수 네이밍의 <span style="color:cornflowerblue">**팁**</span>

많은 유튜브 채널이나 교재에서 변수 이름에 대해 "<span style="color:cornflowerblue">**변수 이름만 봐도 무슨 목적인지 명확히 알 수 있어야한다.**</span>" 라고 한다. 지나치게 간소화하거나 본인 임의로 지은 변수명은 불필요한 주석이 계속 붙어 가독성을 떨어트리거나, 시간이 지난 후 코드를 파악하는데 시간이 걸리게 만들기 때문이다.
```javascript
var X = 10;  // X가 무엇을 의미하는 변수인지 알 수 없다.
var score = 15;  // 'score'라는 이름을 봤을 때 점수를 의미하는 것을 알 수 있다.
```
의미가 불분명하여 주석이 많은 식별자는 좋은 식별자가 아니라는 점을 기억해두자.

---
### <span style="color:cornflowerblue">**네이밍 컨벤션(Naming Convention)**</span>
네이밍 컨벤션은 하나 이상의 영어 단어로 구성된 식별자에서 가독성을 향상시키기 위해 규정한 규칙이다. 다음과 같은 네이밍 컨벤션이 자주 사용된다.
```javascript
var appleTree; // 카멜 케이스(camelCase)
var apple_tre0e; // 스네이크 케이스(snake_case)
var AppleTree; // 파스칼 케이스(PascalCase)
```
일반적으로 Javascript에서는 변수나 함수의 이름에는 '**카멜 케이스(camelCase)**'를 사용하고, 생성자 함수, 클래스(class)의 이름에는 '**파스칼 케이스(PascalCase)**'를 주로 사용한다고 한다.


<br><br>
<br>
> 이번엔 간단한 네이밍 규칙을 알아봤다. 그렇지만 찾아보니 개발자들이 주로 쓰는 언어별 식별자가 별도로 존재하는 것 같다. 다음엔 더 자세하게 식별자 작성 팁을 공부해봐야 겠다.

