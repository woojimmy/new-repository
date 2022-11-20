---
title: "[Javascript] - class 사용해보기"
excerpt: "Javascript에서 class를 선언, 활용하는 방법을 알아보자."

categories: 
  - Javascript
tags: [Javascript, class, object]
toc: true
author_profile: true 
sidebar:
   nav: "docs"
---

# Javascript의 class

## class와 object의 차이점
`class`는 `object`를 생성하는 template이다. <br> 
인터넷에서 가장 흔한 비유인 '붕어빵'을 예시로 들자면
- 붕어빵 틀(`class`) -> 팥 -> 팥 붕어빵(`object`)
- 붕어빵 틀(`class`) -> 크림 -> 크림 붕어빵(`object`)

## class 사용해보기
### 개요
```javascript
let wecode1 = {
  listName: "we_are_beer",
  listImage: "url('/students/40th/woojin/story_image/beer-g499257807_640.jpg')",
  listRealName: "beer Kim",
};

let wecode2 = {
  listName: "we_are_cake",
  listImage: "url(/students/40th/woojin/story_image/cake-g46e278bc6_640.jpg)",
  listRealName: "cake Lee",
};
let wecode3 = {
  listName: "wecode",
  listImage: "url(/students/40th/woojin/story_image/code-ga3929d1d3_640.jpg)",
  listRealName: "wecode!!!!!!",
};
let wecode4 = {
  listName: "we_love_rabbits",
  listImage: "url(/students/40th/woojin//main_recommendation_image/rabbits-g43fed7b42_640.jpg)",
  listRealName: "rabbits Woo",
};

const searchListArr = [
    wecode1,
    wecode2,
    wecode3,
    wecode4,
];
```
<img src="/assets/images/20221120/searchbar-list.png"> <br>
instagram 클론을 하면서 검색창에 여러 profile을 뜨게 하기 위해 <br>
위의 코드처럼 objects를 생성하고, array로 만들었다. <br>
그 이유는 `forEach`로 array에 있는 objects를 load할 때, 입력한 data를 한 번에 보이게 만들면 data 관리가 더 쉬울 것이라 생각했기 때문이다. <br>
처음에는 array에 모든 objects를 직접 입력했었는데, 가시성이 상당히. 심각하게 안좋아서 이렇게 모두 선언문 식으로 바꿨다.<br>
(그런데 이것도 그닥 좋아보이지는 않는다..)<br>
그래서 이번엔 `class`를 배운 김에 더 간단하고 짧고 읽기 쉽게 object를 생성해보려 한다.

### 코드 생성, 뜻 밖의 오류
```javascript
class Person {
  constructor(profile, imageUrl, name) {
    this.listName = profile;
    this.listImage = url(imageUrl);
    this.listRealName = name;
  }
}
```
제일 처음 입력했던 objects를 주석처리하고 다음과 같은 코드를 입력하였다. <br>
일단 object를 하나만 만들어 넣어보자.
```javascript
const wecode1 = new Person(
  "we_are_beer",
  "/students/40th/woojin/story_image/beer-g499257807_640.jpg",
  "beer Kim"
);

const searchListArr = [
    wecode1    
];
```
<img src="/assets/images/20221120/searchbar-list2.png"> <br>
음? 나오지 않는다?<br><br>
<img src="/assets/images/20221120/searchbar-list3.png"> <br>
아... class 선언문에 url을 인식 못한다.. <br>
`wecode1`의 imageUrl value를 'url(경로)'로 만들면 바로 해결되겠지만, <br> 
이미지 파일 경로만 입력하면 되게 만들고 싶다.

```javascript
    this.listImage = 'url' + (imageUrl);
```
이렇게 바꿔보았지만, 여전히 되지 않는다. <br><br>
<img src="/assets/images/20221120/searchbar-list4.png"> <br>
이번엔 창은 뜨지만, 사진이 나오지 않는다. <br> 사진 부분을 개발자 도구로 확인해보니 <br><br>
<img src="/assets/images/20221120/searchbar-list5.png"> <br>
`background-image`의 형식이 잘못 되어있다. <br>
`imageUrl`을 괄호(`()`) 안에 넣어서 될 줄 알았는데, 괄호는 인식이 안되나 보다.
<br>

```javascript
    this.listImage = 'url'+'('+imageUrl+')';
```
괄호를 어떻게하면 넣을 수 있을까 고민하다 다음과 같이 입력해 보았다.
<br><br>
<img src="/assets/images/20221120/searchbar-list6.png"> <br>
성공!!!! <br>
이제 다른 object도 만들어주자. <br><br>

```javascript
const wecode1 = new Person(
  "we_are_beer",
  "/students/40th/woojin/story_image/beer-g499257807_640.jpg",
  "beer Kim"
);
const wecode2 = new Person(
  "we_are_cake",
  "/students/40th/woojin/story_image/cake-g46e278bc6_640.jpg",
  "cake Lee"
);
const wecode3 = new Person(
  "wecode",
  "/students/40th/woojin/story_image/code-ga3929d1d3_640.jpg",
  "wecode!!!!!!"
);
const wecode4 = new Person(
  "we_love_rabbits",
  "/students/40th/woojin//main_recommendation_image/rabbits-g43fed7b42_640.jpg",
  "rabbits Woo"
);
```
<img src="/assets/images/20221120/searchbar-list7.png"> <br>

### 결론
물론, 여전히 길지만 `class`를 통해 배운 점을 정리하자면, 
- key의 중복이 사라져 key가 많을수록 효과적이라 생각하고,
- key를 변경하고 싶을 때 각 object마다 모든 key를 수정하지 않아도 되서 유지보수에도 좋은 것 같다.

이번에 `class`를 처음 써봤는데, 오늘 사용한 `contributor` 외에도 `setter`, `getter`, `static`, `inheritance` 등 여러 기능에 대해서도 더 공부해서 이해하도록 하자.











