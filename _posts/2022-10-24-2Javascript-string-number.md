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

# 문자열 + 숫자 = ?
## 순서에 따라 다른 값
```javascript
console.log('2' + 2 + 2);  //  ---???
```
위 코드는 어떻게 출력될까??<br> 문자 2와 숫자 2의 연산이니 `'2'+ (2 + 2)`라고 생각해 `24`가 나올 것이라 예상할 수 있다. <br> **그러나 결과는 `222`가 나온다.**<br>
<img src="/assets/images/20221018/stringnumber.png"> <br>
왜일까..? 숫자는 숫자끼리. 문자는 별개로 처리되어야 하는게 아닐까???<br>`console.log(3 + 2 + '2');`는 `52`라는 결과가 나온 것과 비교하면 이해가 되지 않는다.<br>
<img src="/assets/images/20221024/stringplusnumber1.png">

## 연산의 순서
이 결과를 이해하기 위해서는 두 가지를 알아야 한다.
- 괄호와 같은 특별한 경우가 아니면 연산은 앞에서부터 순서대로 시행된다.
- '문자열(string)'+ '숫자(number)' = '문자열'이다.

```javascript
let number = 3 + 2 + '2';
console.log(number); //  --- 52
```
변수 `number`에서 앞의 숫자 `3`과 `2`가 앞에 있으므로, 숫자의 연산이 먼저 이루어진다. 즉, `5`라는 숫자 값이 먼저 연산된 후에 `'2'`라는 문자열과의 연산이 이루어진다. <br> 그렇게 숫자`5`와 문자열 `'2'`가 더해져 `52`라는 **문자열**의 값이 나오는 것이다.<br> 그런데 이게 문자열인지 아닌지 확인해봐야 안심할거같다.
```javascript
console.log(number == 52); // --- true
console.log(number === 52); // --- false
```
<img src="/assets/images/20221026/operator1.png"> <br>
`number`라는 변수는 `52`라는 값을 가지기에 `==`를 이용했을 때는 `true`가 출력된다. 그렇지만 `52`는 숫자가 아닌 문자열이기 때문에 `===`를 사용했을 때는 `false`가 출력된다.
```javascript
console.log(number === '52'); // --- true
```
<img src="/assets/images/20221026/operator2.png"> <br> `52`를 문자열로 바꾸니 `true`가 출력되는 것을 볼 수 있다.<br><br>

------
```javascript
let number2 = '3' + 2 + 2;
console.log(number2); // --- 322
```
이 코드에서는 가장 처음부터 `문자열 + 숫자`의 연산이 등장한다. 그렇게되면 `'3'`과 `2`를 더해 `32`라는 문자열의 값이 생기고, 여기에 숫자 `2`를 더하는 순서로 연산이 이루어진다. 그러나 이미 `32`는 문자열과 숫자가 더해진 **문자열**의 값이다. 그러므로 그 다음 연산 또한 `문자열 + 숫자`이게 된다. 그렇기 때문에 `322`라는 문자열의 값이 출력되는 것이다.
```javascript
console.log(number2 == 322); //  --- true
console.log(number2 === 322); // --- false
console.log(number2 === '322'); //  --- true
```
<img src="/assets/images/20221026/operator3.png"> <br> 역시 확인해보면 `322`가 문자열인 것을 알 수 있다.<br>

## 응용
여기서 우리는 연산 중 '문자열'과 '숫자'가 만나는 순간에 '문자열'로 변하는 것을 확인했다. 그렇다면 `숫자 + 숫자 + 문자열 + 숫자 + 숫자`의 경우에는 어떨까?<br> 아마 예측하건데 문자열보다 뒤에 있는 숫자들은 숫자로 연산되지 않을 것이다. 직접 한 번 확인해보자.
```javascript
let number3 = 2 + 2 + '3' + 4 + 5 + 6;
console.log(number3); // --- 43456
```
<img src="/assets/images/20221026/operator4.png"> <br> 역시 앞의 `2+2`는 숫자로 연산되었지만 문자열 `'3'`과 만나면서 문자열로 바뀌고, 뒤의 숫자들은 숫자로 연산되지 않았다.<br><br>
<img src="/assets/images/20221026/operator5.png"> <br> 확인해보니 문자열이 맞다.

## 다른 연산자는??
console.log들을 쳐보면서 다른 연산자도 `+`와 동일하게 작동하는지 궁금해졌다.
### '-' 
```javascript
let number4 = 2 + 2 - '2' + 3;
let number5 = 3 - 2 + '2' + 3;
let number6 = '2' - 2 + 3;
let number7 = '2' + 2 - 2 + 3;

console.log(number4);  //  ---5
console.log(number5);  //  ---123
console.log(number6);  //  ---3
console.log(number7);  //  ---23
```
왜 4번이나 했냐면,
- number4: 연산 '중간'에 문자열이 있고, 문자열에 `-`가 붙은 경우.
- number5: 연산 '중간'에 문자열이 있고, 문자열에 `-`가 붙지 않은 경우.
- number6: 연산 '처음'에 문자열이 있고, 문자열에 `-`가 붙은 경우.
- number7: 연산 '처음'에 문자열이 있고, 문자열에 `-`가 붙지 않은 경우.

이렇게 4가지를 생각했다.
```javascript
console.log(typeof number4);  //  ---number
console.log(typeof number5);  //  ---string
console.log(typeof number6);  //  ---number
console.log(typeof number7);  //  ---number
```
각 결과의 타입과 결과들을 보면 다음과 같은 사실을 알 수 있다.
- 문자열에 `-`연산자가 붙으면 그 결과는 `number`로 처리된다.
- 문자열보다 앞의 숫자 연산은 숫자로 이루어진다.
- 문자열 뒤에 `-`연산자가 있으면 그 결과는 `number`가 된다.

`number5`에서는 앞의 `3-2`가 숫자로 연산되어 `1`이란 `number`의 결과가 먼저 도출되고, 이후에 `1`과 문자열 `'2'`가 합쳐지므로 `string`으로 변환된다.

### '*', '/'
```javascript
let number4 = 2 + 2 * '2' + 3;
let number5 = 3 * 2 + '2' + 3;
let number6 = '2' * 2 + 3;
let number7 = '2' + 2 * 2 + 3;

console.log(number4);  //  ---9
console.log(number5);  //  ---623
console.log(number6);  //  ---7
console.log(number7);  //  ---243

console.log(typeof number4);  //  ---number
console.log(typeof number5);  //  ---string
console.log(typeof number6);  //  ---number
console.log(typeof number7);  //  ---string
```
`*`와 `/`는 동일하게 작동하므로 한 가지만 실행해봤다. 이 결과로 다음과 같은 사실을 알 수 있다.
- 문자열에 `연산자`가 붙으면 `number`가 된다.
- 문자열에 `연산자`가 붙지 않으면, `string`이 된다.
중요한 점은 `-`는 문자열 뒤에 연산 중간에 있어도 그 결과가 `number`로 변환되었지만, `*`와 `/`는 `string`이 된다는 점이다. 이 차이점을 기억해두자.
