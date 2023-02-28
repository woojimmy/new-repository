---
title: "[Javascript] - `Array.sort()`메서드와 CompareFunction"
excerpt: "Javascript에서 sort()메서드와 이 함수 안에서 어떠한 것을 매개변수로 받는 CompareFunction에 대해 알아보고, sort()메서드의 작동원리를 이해해보자"

categories:
  - Javascript
tags: [Javascript, theory, function, sort, method]
toc: true
author_profile: true
sidebar:
  nav: "docs"
---

# Array.sort(CompareFunction)

코딩테스트 문제를 풀다가 array를 정렬해주는 `.sort()`메서드에 대해 알게 되었다. <br> 그런데, 이 함수의 parameter에 <span style="color: cornflowerblue">`compareFunction`</span>을 입력해야만 하는 상황이 있었고, 이 `compareFunction`를 이해하기 위해 브라우저에 console.log를 이용해 여러 방법으로 실행해보았다. <br>
참고로 `sort()`에 대한 개념 정리 글이 아님을 미리 밝힌다.

## Array.sort()

> `sort()`메서드는 array의 index를 적절한 위치에 정렬한 후, 그 array를 return한다. 기본 정렬 순서는 string의 유니코드 코드 포인트를 따른다. - mdn web docs

### 예시

```javascript
let arr1 = [2, 0, 8, 3];
let arr2 = ["banana", "mango", "apple", "kiwi"];

arr1.sort(); // [0, 2, 3, 8]
arr2.sort(); // ['apple', 'banana', 'kiwi', 'mango']
```

<center><img src='../../../assets/images/20230227/sortBasic.png'></center>
 <br>
위 예시처럼 `sort()`메서드는 배열을 유니코드 순서에 따라 오름차순으로 정렬한다. <br>
매우 간단해 보이지만 이렇게 parameter에 어떠한 함수도 호출하지 않고 사용한다면 다음과 같은 문제점이 발생한다.

### Parameter로 compareFunction 없을 때 문제점

```javascript
let arr3 = [5, 0, 10, 200, 9];

arr3.sort(); // [0, 10, 200, 5, 9]
```

<center><img src='../../../assets/images/20230227/sortBasic2.png'></center>
 <br>
분명 우리는 number로 index를 입력하였다. 그렇기 때문에 순서대로 정렬하면 <br>`[0, 5, 9, 10, 200]` <br>이렇게 나와야할 것 같은데, 우리가 원하지 않는 결과가 출력되었다. <br>
그 이유는 <span style="color: cornflowerblue">**`sort()`메서드에서 각 index를 string화 한 뒤, 첫 글자를 기준으로 해당 index의 위치를 판단하기 때문이다.**</span> <br>
즉, number `200`은 string `'200'`이 되어 다음 index인 string `'5'`와 비교해 `'5'`가 `'2'`보다 유니코드 상 더 큰 글자이기 때문에 `200`이 `5`보다 더 앞에 오게 되는 것이다.

## CompareFunction

### CompareFunction 기본적인 이해

> `CompareFunction`이 제공되면 index는 compare 함수의 return 값에 따라 정렬된다. `a`와 `b`가 비교되는 두 index라면,
>
> - `compareFunction(a, b)`이 0보다 작은 경우 `a`를 `b`보다 낮은 index로 sort. 즉, `a`가 먼저 온다.
> - `compareFunction(a, b)`이 0을 return하면 `a`와 `b`를 서로에 대해 변경하지 않는다.
> - `compareFunction(a, b)`이 0보다 큰 경우, `b`를 `a`보다 낮은 index로 sort한다. 즉, `b`가 먼저 온다.
>   <br> <span style="float: right">- mdn web docs</span>

<br>
간단히 말하면 다음과 같다. <br>

- `compareFunction`은 2개의 index를 parameter로 받는다.
- `compareFunction(a, b)`가 **음수**를 return하면 **[a, b]**. 즉, **`a`가 `b` 앞에 온다**
- `compareFunction(a, b)`가 **양수**를 return하면 **[b, a]**. 즉, **`b`가 `a` 앞에 온다**
- `compareFunction(a, b)`가 **0**을 return하면 **`a`와 `b`의 위치는 변하지 않는다.**

여기서 궁금증이 생겼다. <br>
CompareFunction은 parameter를 2가지를 받는다고 했다. <br>
그런데 index가 3개 이상으로 많은 array에서 어떻게 parameter를 받는 것인가??? <br>
역시 궁금할 땐 `console.log`아니겠는가

### CompareFunction의 paramter와 작동 확인

```javascript
let arr = [5, 3, 1, 2];

arr.sort(function (a, b) {
  console.log(`a는 바로 ` + a + `, 그리고 b는 ` + b);
});
// a는 바로 3, 그리고 b는 5
// a는 바로 1, 그리고 b는 3
// a는 바로 2, 그리고 b는 1

console.log(arr); // [5, 3, 1, 2]
```

<center><img src='../../../assets/images/20230227/compareFunction.png'></center> <br>

`console.log`를 통해 다음과 같은 사실을 알아냈다.

1. `compareFunction(a, b)`는 2개의 연속된 index를 인자로 받는다.
2. 첫 번째 인자인 `a`는 연속된 index 중 뒤에 있는 것이다.
3. 두 번째 인자인 `b`는 연속된 index 중 앞에 있는 것이다.

또한, sort()메서드 이후에도 `console.log`를 보면 arr의 index가 재정렬되지 않았다. <br>
이것은 comparefunction인 익명의 function이 어떠한 값도 출력하고 있지 않기 때문이다. <br>
이 function이 어떠한 value를 return해야 arr가 정렬될 수 있을 것이다. <br>

---

<span style="color:crimson">**_그러나!!!_**</span><br>
무엇인가 이상하지 않은가??<br>
분명 `console.log`에 대한 출력값을 보면, 연속된 index끼리 비교하는 것처럼 보인다. <br>
그런데 만약 연속된 index끼리만 비교한다면, 전체 array가 오름차순으로 정렬되는게 가능할까??? <br>

```javascript
let array = [5, 3, 1, 9];
```

만약 위 예시에서 `5`와 `3`과 `1`을 비교하는 연산을 통해 `[1, 3, 5]`라는 결과까지 완성되었다고 가정하자. <br>
그렇다면 다음에 `1`과 `9`를 비교하는 연산을 해야하는데, 여기서 `1`보다 높은 index 자리를 가진 `9`의 위치를 특정할 수 있는가? <br>
<span style="color:crimson">즉, 연속된 index끼리의 비교 연산으로는 정렬이 불가능하다</span>는 얘기다. <br><br>

### CompareFunction과 sort()의 원리 알고싶다...

무엇을 잘못한 것일까...(진짜 한참을 고민&검색했다)<br>
정렬과 관련된 함수를 입력하지 않아서 정렬할 필요가 없어서 그런 것일 수도 있을 것이라 생각했다.<br>
오름차순으로 정렬할 수 있게 다시 입력해보자..ㅠㅠ!

```javascript
let arr = [0, -1, 2, 1];

arr.sort((a, b) => {
  console.log(a, b);
  return a - b;
});
```

<center><img src='../../../assets/images/20230227/compareFunction2.png'></center> <br>
CompareFunction은 이제 편하게 arrow function으로 쓰기로 하고, 결과를 보면<br>
비교하는 경우가 더 많아졌다! <br>
즉, **`sort()`에서 `compareFunction`은 연속된 index를 비교하는 것이 아니었다!** <br>
나는 이 코드를 실행하기 전, `sort()`메서드는 각 index를 각각 모두 비교해서 배열을 정렬한다고 생각했다. <br>
그러나, 내 생각이 맞다면 비교의 수가 6개(index가 4개, 경우의 수는 `4 * 3 / 2 = 6` ).<br>
즉, `console.log`에 6가지의 결과가 출력되어야 한다. <br>
그러나 내가 입력한 console 창에는 5가지의 결과만 출력되었다.

```javascript
let arr = [-1, 0, 1, 2];

arr.sort((a, b) => {
  console.log(a, b);
  return a - b;
});
```

<center><img src='../../../assets/images/20230227/compareFunction3.png'></center> <br>
이번에는 배열에서 index의 순서만 바꾼채 동일한 `sort()`메서드를 적용해보았다.<br>
그런데 console 창에는 3가지의 결과만 출력된다.<br>
이건 마치 위에 `compareFunction`에 정렬 함수 없이 `console.log`만 입력했을 때와 비슷하다.

```javascript
let arr = [-1, 0, 1, 2];

arr.sort((a, b) => {
  console.log(a, b);
  if (b % 2 === 0) {
    return a - b;
  } else if (a % 2 === 0) {
    return b - a;
  }
});
```

<center><img src='../../../assets/images/20230227/compareFunction4.png'></center> <br>
이번에는 완전 동일한 배열에 `compareFunction`만 바꿔보았다. <br>
홀수, 짝수에 따라 정렬하는 로직인데, 여기서는 console.log에 5가지가 출력이 된다.
<br><br>

일단, 여기서 알 수 있는 점은 내가 처음 생각한 **`sort()`메서드는 각 index를 모두 비교해서 정렬한다**라는 가정은 틀렸다는 것이다.<br>
정확하게 설정된 로직을 알 수 없었지만, `sort()`메서드는 정렬하는 과정에서 index끼리 비교하는 연산을 하되,<br>
메서드에서 설정된 로직에 따라 전체 index끼리 비교하는 것이 아닌,<br>
어떠한 조건을 충족하면 특정 index끼리는 비교 연산을 거치지 않도록 짜여져 있다고 유추해 볼 수 있을 것 같다.<br>
어쩌면 이 과정들이 index를 정렬하기 위한 최적, 최소의 연산을 행할 수 있도록 만들어졌을 수도 있겠다라는 생각이 들었다.

## 메서드 로직에 대해 고민, 공부하며 느낀점

아직 개발이라는 분야를 시작한지 얼마 되지 않았지만, 그 동안 포스팅했던 것 중 가장 고민을 많이 했던 것 같다.<br>
분명 저 `compareFunction`의 매개변수가 어떤 로직(또는 알고리즘)으로 동작하는지 알 방법이 있을 것 같은데,<br>
아직 나의 실력과 경험 부족으로 방법을 찾지 못한 것 같아 너무 아쉬운 마음이다.<br>
구글링하며 `javascript의 sort 알고리즘` 이라는 이름으로 수 많은 글들을 봤지만,<br>
해당 글의 코드들이 직접 javascript에서 sort하기 위한 알고리즘을 짠 것인지,<br>
아니면 V8엔진에서 그 코드의 방식대로 작동하는 것인지 지금의 내가 판단하기에는 불분명했다.<br>
아직 많이 부족하다는 것을 느끼며, 이런 메서드 작동 원리를 파악하는 방법을 배워보고 싶다.
