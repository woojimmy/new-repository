---
title: "Javascript 기초 이론 - 변수(Variable)"
excerpt: "Javascript의 '변수'에 대해 기초적인 지식을 다뤄보자."

categories: 
  - posting
tags: [Javascript, theory, variable]
toc: true
author_profile: true 
sidebar:
   nav: "docs"
---


# **변수(Variable)**

> 이번 글에서는 변수에 대해 아주 기초적인 개념과 예시를 적을 예정이다. 그러므로 'var'키워드를 이용하여 예시를 작성할 것이며, 'var', 'let', 'const'키워드의 차이점, var보다 let이 권장되는 이유 등의 조금 더 어려운 내용은 더 공부해서 이후 다른 글에 포스팅해보자

## Javascript에서 <span style="color:cornflowerblue">변수</span>란 무엇인가?
> **변수는 하나의 값을 저장하기 위해 확보한 메모리 공간 자체 또는 그 메모리 공간을 식별하기 위해 붙인 이름을 말한다.** <br> <sub> <span style="color:darkgrey">(출처: 모던 자바스크립트 deep dive - 이웅모 지음)</span></sub>

  변수는 쉽게 말하자면 특정한 값에 '이름'을 붙이는 것을 말한다.
  <br>변수를 설명하기 전에 잠깐 <u>메모리</u>와 <u>변수가 왜 필요한지</u>에 대한 설명이 필요하다. 우리가 사용하는 컴퓨터는 CPU를 사용해 연산을 하고, 메모리를 사용해 해당 데이터를 저장한다. 이러한 메모리는 여러 메모리 셀(memory cell)의 집합체이며, 이 셀들은 각각 고유의 주소를 가진다. <br>만약 연산을 통해 어떠한 값을 얻었다면, 이 값은 특정 주소를 지닌 메모리 셀에 저장될 것이다. 그렇다면 우리가 이후에 이 연산된 값을 불러오기 위해선 어떠한 방법을 써야할까? <br> 주소를 통해 저장된 셀에 직접 접근하는 방법을 생각하겠지만, 이는 위험하며 Javascript에서는 개발자의 직접적인 메모리 제어가 불가능하여 어려운 방법이다. 그렇기 때문에 우리는 이 연산된 값에 특정한 '이름'을 지정하여 필요할 때마다 불러낼 수 있게 하는 것이 <span style="color:cornflowerblue">'변수'</span>이다.
<br>


## <span style="color:cornflowerblue">**변수 선언**</span>에 사용되는 키워드

> <span style="color:crimson">**키워드(Keyword)**</span> <br> : Javascript 엔진이 수행할 동작을 규정한 약속된 명령어. 

Javascript에서는 변수를 선언할 때 <span style="color:cornflowerblue">**var, let, const**</span> 세 가지 키워드를 주로 사용한다. 각각의 특징들을 살펴보면
<ol>
<li><font color="cornflowerblue"><b>var</b></font><br> : ES5(ECMAScript) 까지는 주로 쓰인 변수 선언 키워드이다. 여러 단점들로 인하여 2015년 공개된 ES6에서 새로 등장한 let, const키워드로 인해 현재는 권장되지 않으나, ES6 이전 사양으로 작성된 코드는 주로 var 키워드를 이용해 구현되어있다. </li>
<li><font color="cornflowerblue"><b>let</b></font><br> : var 키워드의 단점을 보완하기 위해 ES6부터 등장한 키워드이다. 현재는 var보다 let을 더 권장하며 많이 쓰인다.</li>
<li><font color="cornflowerblue"><b>const</b></font><br> : let과 함께 ES6부터 등장했으나, let과 다른 점은 const 키워드는 재할당이 불가능하다는 것이다. 반드시는 아니지만 주로 상수(constant)를 선언하기 위해 사용한다.</li>
</ol>

<br>

## <span style="color:cornflowerblue">**변수**</span>와 관련된 용어
<ul>
<li><font color="cornflowerblue"><b>변수 이름, 변수명, 식별자(identifier)</b></font><br> : 개발자가 지정하는, 메모리 공간에 저장된 값을 식별할 수 있는 고유한 이름. 식별자는 변수 값이 아닌 메모리 주소를 기억하고 있어야 한다.</li>
<li><font color="cornflowerblue"><b>변수 값</b></font><br> : 지정된 변수에 저장된 값이다.</li>
<li><font color="cornflowerblue"><b>변수 호이스팅(variable hoisting)</b></font><br> : 변수 선언문이 먼저 동작하는 Javascript 고유의 특징을 '변수 호이스팅'이라 말한다.</li>
<li><font color="cornflowerblue"><b>할당(assignment, 대입, 저장)</b></font><br> : 특정 '변수 이름'에 '변수 값'을 저장하는 것이다.</li>
<li><font color="cornflowerblue"><b>선언(declaration)</b></font><br> : 변수를 생성하는 것을 말한다. 값을 저장하기 위한 메모리 공간을 확보하고, 변수 이름과 해당 메모리 공간의 주소를 연결하여 값을 저장할 수 있게 준비하는 것이다. 값을 저장하는 '할당'과는 다른 개념이다.</li>
<li><font color="cornflowerblue"><b>참조(reference)</b></font><br> : 변수에 저장된 '변수 값'을 읽어 들이는 것이다.</li>
</ul>
<br>


### <span style="color:cornflowerblue">**변수 호이스팅(Variable Hoisting)**</span>
```javascript
console.log(example);
var example;
```
Javascript에 console.log(example); 한 줄만 입력하는 것과, 밑에 변수 할당을 함께 입력했을 때 어떠한 차이가 나는지 확인해보자.<br>
<img src="/assets/images/20221006/capture1.png"><br>
console.log(example);만 입력했을 때는 선언하지 않은 식별자에 접근할 때 발생하는 <font color="crimson"><b>'ReferenceError(참조 에러)'</b></font>가 발생했지만, 밑줄에 변수 선언을 추가하자 **undefined**가 출력되었다. Javascript 엔진은 코드를 한 줄씩 순서대로 실행하는데(런타임, runtime) 왜 이런 차이가 일어나는 것일까?<br>그 이유는 Javascript 엔진이 런타임 실행 전에 소스코드의 모든 선언문들을 우선적으로 실행하기 때문이다. 그렇기 때문에 비록 밑에 있더라도 변수 선언이 먼저 실행되어 'example'이라는 이름의 변수가 할당되어 <font color="crimson"><b>참조 에러</b></font>가 아닌 **undefined**가 출력이 된 것이다. 이러한 작동 특징을 <span style="color:cornflowerblue">'변수 호이스팅'</span>이라 한다.

### <span style="color:cornflowerblue">**할당(Assignment)**</span>
```javascript
var example; // 변수를 선언.
example = 75; // 선언된 변수에 값을 할당.
```
```javascript
var example = 75; // 변수 선언과 값의 할당.
```
변수에 값을 할당할 때는 `=` 을 사용한다. 위의 2개로 나눈 코드와 밑의 1줄인 코드는 동일하게 작동한다.<br> <span style="color:crimson">**하지만!**</span> 주의해야 할 점은 한 1줄로 코드를 입력해도 '선언'과 '할당'은 작동 시점이 다르다. 이처럼 같은 줄에 있다 하더라도 **'변수 선언'은 런타임 이전에, '할당'은 런타임에** 실행된다. 다음과 같은 코드를 입력해보자
```javascript
console.log(example); // A
var example; // B
example = 75; // C
console.log(example); // D
```
<img src="/assets/images/20221006/capture2.png"><br>
위에서는 2가지 값이 나온다. 이 값들은 <span style="color:cornflowerblue">console.log(example);</span>의 값이며, 하나는 'undefined', 다른 하나는 75가 출력되었다. 만약 선언(**B**) 이후 런타임 이전에 할당(**C**)이 실행되었다면 **A**의 console.log 또한 75의 값이 출력되어야 한다. 그러나 **A**는 'undefined'가 출력되었고, 이는 example이라는 변수가 아직 값을 할당받지 못했다는 것을 의미한다. 반면에 **D**의 console.log는 75라는 값을 할당받았기에 위 코드의 진행 순서는 다음과 같다.
```javascript
console.log(example); // A ----- 2번째
var example; // B ----- 1번째
example = 75; // C ----- 3번째
console.log(example); // D ----- 4번째
```
이를 통해 변수 선언(**B**) 이외의 코드는 모두 런타임에서 작동한 것을 알 수 있다.

### <span style="color:cornflowerblue">**재할당과 상수(Constant)**</span>
재할당이란 기존에 있는 변수에 새로운 값을 다시 할당하는 것이다.
```javascript
var example = 75;
console.log(example);
example = 95;
console.log(example);
```
<img src="/assets/images/20221006/capture3.png"><br>
첫 번째에서 변수 example은 75라는 값을 할당받았고, 정상적으로 출력되었다. 두 번째에서 변수에 할당된 값을 95로 바꿔도 문제 없이 작동했다. 이처럼 <span style="color:cornflowerblue">**var**</span> 키워드로 선언한 변수는 선언과 동시에 'undefined'로 초기화 되기 때문에 재할당이 가능하다.(애초에 "변수"이지 않은가)<br> 그러나 재할당을 금지시킬 수도 있다. 이러한 것을 <span style="color:cornflowerblue">**'상수(constant)'**</span>라고 하며, 단 한 번만 할당받을 수 있는 변수를 말한다. 상수를 입력하기 위해서는 <span style="color:cornflowerblue">**const**</span>키워드를 사용한다. 아래 코드를 보자
```javascript
const example = 75;
console.log(example);
example = 95;
console.log(example);
```
<img src="/assets/images/20221006/capture4.png"><br>
<span style="color:cornflowerblue">**const**</span>키워드를 사용하여 선언된 변수는 재할당이 금지된다. 그렇기 때문에 변수 example은 처음 할당된 75는 정상적으로 출력되었지만, 95로 재할당하고자 했을 때는 이는 이미 상수가 되었기 때문에 에러가 발생했다. 그리고 변수 example의 값을 확인하니 처음 할당된 '75'가 변하지 않았음을 알 수 있다.

---

<br><br>
<br>
> 원래 식별자 이름 짓는 규칙까지 이번 글에서 작성하려 했으나, 글이 생각보다 길어졌다... ㅎㅎ;; ~~이번엔 여기서 마치고 식별자 네이밍은 다음에 다시 작성해 링크로 걸어야겠다.~~ 잔디 화이팅~~!!

네이밍 규칙 게시글 링크↓<br>
<a href="https://woojimmy.github.io/posting/javascript-variable-name/" target="_blank">변수 네이밍(variable naming)규칙</a>

