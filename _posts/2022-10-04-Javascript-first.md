---
title: "Javascript 이론 - 변수(Variable)"
excerpt: "Javascript의 이론 중 '변수'에 대해 다뤄보자."

categories: 
  - posting
tags: [Javascript, theory, variable]
toc: true
author_profile: true 
sidebar:
   nav: "docs"
---
# 변수(Variable)

## Javascript에서 <span style="color:cornflowerblue">**변수**</span>란 무엇인가?
> 변수는 하나의 값을 저장하기 위해 확보한 메모리 공간 자체 또는 그 메모리 공간을 식별하기 위해 붙인 이름을 말한다. <sub> <span style="color:darkgrey">(출처: 모던 자바스크립트 deep dive - 이웅모 지음)</span></sub>

  변수는 쉽게 말하자면 특정한 값에 '이름'을 붙이는 것을 말한다.
  <br>변수를 설명하기 전에 잠깐 <u>메모리</u>와 <u>변수가 왜 필요한지</u>에 대한 설명이 필요하다. 우리가 사용하는 컴퓨터는 CPU를 사용해 연산을 하고, 메모리를 사용해 해당 데이터를 저장한다. 이러한 메모리는 여러 메모리 셀(memory cell)의 집합체이며, 이 셀들은 각각 고유의 주소를 가진다. <br>만약 연산을 통해 어떠한 값을 얻었다면, 이 값은 특정 주소를 지닌 메모리 셀에 저장될 것이다. 그렇다면 우리가 이후에 이 연산된 값을 불러오기 위해선 어떠한 방법을 써야할까? <br> 주소를 통해 저장된 셀에 직접 접근하는 방법을 생각하겠지만, 이는 위험하며 Javascript에서는 개발자의 직접적인 메모리 제어가 불가능하여 어려운 방법이다. 그렇기 때문에 우리는 이 연산된 값에 특정한 '이름'을 지정하여 필요할 때마다 불러낼 수 있게 하는 것이 <span style="color:cornflowerblue">'변수'</span>이다.


## <span style="color:cornflowerblue">**변수**</span>와 관련된 용어
<ul>
<li>변수 이름(변수명)</li> : 개발자가 지정하는, 메모리 공간에 저장된 값을 식별할 수 있는 고유한 이름
<li>변수 값</li> : 지정된 변수에 저장된 값
<li>할당(assignment, 대입, 저장)</li> : 특정 '변수 이름'에 '변수 값'을 저장하는 것
</ul>

