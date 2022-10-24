---
title: "[Javascript] 이론 - 숫자와 문자열의 연산"
excerpt: "Javascript에서 숫자와 문자열의 연산시 특이사항에 대해 공부해보자."

categories: 
  - Javascript
tags: [Javascript, theory, string, number]
toc: true
author_profile: true 
sidebar:
   nav: "docs"
---

# 데이터 타입(Data type)



### 주의해야할 것 (문자 + 숫자의 조합)
```javascript
console.log('2' + 2 + 2);  //  ---???
```
그렇다면 위 코드는 어떻게 출력될까??<br> 문자 2와 숫자 2의 연산이니 `'2'+ (2 + 2)`라고 생각해 `24`가 나올 것이라 예상할 수 있다. <br> **그러나 결과는 `222`가 나온다.**<br>
<img src="/assets/images/20221018/stringnumber.png"> <br>
왜일까..? 숫자는 숫자끼리. 문자는 별개로 처리되어야 하는게 아닐까??? 위에서 `console.log(3 + 2 + '2');`는 `52`라는 결과가 나온 것과 비교하면 이해가 되지 않는다. 그래서 console.log를 이용해 차이점을 알아봐야겠다.