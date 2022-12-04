---
title: "[React] - console.log로 알아보는 React의 리랜더링"
excerpt: "React에서 로그인 페이지를 만들고, console.log 위치로 리랜더링에 대해 이해해보자"

categories:
  - React
tags: [react, re-rander]
toc: true
author_profile: true
sidebar:
  nav: "docs"
---

# React에서의 리랜더링

## 로그인 Page의 code

```javascript
import React, { useState } from "react";
import "./App.css";

function Login() {
  const [email, setEmail] = useState("");

  const saveUserId = (event) => {
    setEmail(event.target.value);
  };

  return (
    <div>
      <input
        type="text"
        placeholder="사용자 이메일"
        value={email}
        onChange={saveUserId}
      />
      <input type="password" placeholder="비밀번호" />
      <button>로그인</button>
    </div>
  );
}

export default Login;
```

위 코드에서 email 입력창의 value를 console.log로 찍고 싶다.
<br />
어디에 console.log를 입력해야 내가 원하는 console.log가 출력될까?

## console.log로 변경된 state가 출력되지 않는다?

```javascript
const saveUserId = (event) => {
  setEmail(event.target.value);
  console.log(email);
};
```

input 창에 설정한 onChange의 이벤트 함수에 console.log를 입력해봤다.
<br />
<img src="/assets/images/20221204/reactrerander1.gif"/>
<br />
문제가 발생한다. 1글자씩 없이 console.log가 찍힌다.
<br /><br />
**이게 과연 내가 setState함수를 잘못 사용해서 state가 변경 되지 않는 것인가?
<br />
아니면 변경된 state를 확인하는 console.log의 위치가 잘못된 것인가?**
<br /><br />
만약 전자라면 나중에 button을 활성화하는 함수, 이벤트를 발생 시 입력한 text를 제대로 인식 못하는 문제가 발생 할 수 있어서 확실한 원인을 찾을 필요가 있을 것 같았다.

### - 잘못된 setState 함수(?)

변경된 state를 확실하게 확인할 방법이 무엇이 있을지 고민해봤다.
<br />
만약 onChange 이벤트 밖에서 console.log를 실행한다면 확실히 state가 변경됐는지 확인할 수 있지 않을까?라는 생각이 들었다.
<br />
그래서 로그인 버튼에 onClick 이벤트를 줘서 console.log를 출력할 수 있게 만들어봤다.

```javascript
function Login() {
  const [email, setEmail] = useState("");

  const saveUserId = (event) => {
    setEmail(event.target.value);
  };
  // console.log를 출력하는 이벤트 함수 생성
  const checkEvent = (event) => {
    console.log(email);
  };

  return (
    <div>
      <input
        type="text"
        placeholder="사용자 이메일"
        value={email}
        onChange={saveUserId}
      />
      <input type="password" placeholder="비밀번호" />
      {/* button tag에 onClick으로 위 이벤트 호출 */}
      <button onClick={checkEvent}>로그인</button>
    </div>
  );
}
```

Component 안에 위와 같이 이벤트 발생 함수를 선언, 로그인 버튼에 호출하였다.
<br />
이렇게하면 input창에 입력한 value가 state로 변경된 후에 onClick으로 email의 state를 확인하기에, 정확히 state가 제대로 변경되는지 확인할 수 있을 것이다.
<br />
<img src="/assets/images/20221204/reactrerander2.gif"/>
<br />
로그인 버튼을 클릭할 때마다 input창에 적힌 text가 잘 출력되는 것을 확인했다.
<br />
다행히 setState가 잘못되어 있지는 않았다.
<br />
state는 적절히 저장되고 있던 것.
<br />

### - 잘못된 console.log 위치(!)

setState의 문제가 아니라면 console.log의 위치가 문제일 것이다.
<br />
onChange 이벤트에 넣은 console.log는 이벤트 발생 후 변경된 state를 제대로 반영하지 못한다는 것.

```javascript
const [email, setEmail] = useState("");

const saveUserId = (event) => {
  setEmail(event.target.value);
  console.log(email);
};
```

위에서 작성한 코드를 다시 보자.
<br />
내가 이렇게 작성한 이유는 다음과 같다.

1. saveUserId는 event가 발생할 때 실행되는 함수이다.
2. event가 발생하는 target의 value를 setEmail함수를 통해 email의 state를 변경한다.
3. setEmail을 통해 변경된 email을 event가 발생할 때마다 console.log로 출력한다.

<span style="color: cornflowerblue">그렇지만, 내 예상과 달리 이벤트로 인해 변경된 email이 출력되지 않았다.</span>
<br />
한 글자씩 없이 출력된다는 것은, onChange 이벤트가 발생하면서 state가 변경된 email이 아닌, 기존 state의 email이 출력되는 것이라 생각했다.
<br />
(이벤트 발생 전 이미 input창에 존재하는 value가 출력된다는 것을 의미)
<br /><br />
**여기서 알 수 있는 점은 이벤트 함수가 실행 중에는 state 변경이 저장되지 않는다는 것이다.**
<br /><br />
혼란스러웠다.
<br />
Vanilla JS에서는 이벤트가 잘 작동하는지 확인하기 위해 이벤트 함수에 console.log를 입력해 확인했었다. 그렇지 않으면 page가 load되면서 처음에 단 1번의 console.log만 출력되고, 아무리 이벤트를 실행해도 console.log가 출력되지 않았기 때문이다.
<br /><br />

## React의 중요한 특징 - 리랜더링

React를 배우며 그렇게 들었던 `리랜더링`!!
<br />
Component에 변화가 있을 때마다 리랜더링이 발생하는 React의 중요한 특징을 생각하지 못하고 있었다.
<br />
즉, React에서는 굳이 이벤트 함수 안에 console.log를 찍을 필요가 없다는 것...
<br /><br />
Component 안에 함수나 변수에 포함되지 않은. 그냥 console.log를 입력한다면
<br />

1. onChange 이벤트가 발생할 때마다 Login이라는 Component는 리랜더링되고,
2. 랜더링이 다시 실행되며 Component안에 있는 console.log도 랜더링마다 출력될 것이다.
3. 이벤트 발생 -> state 변경 -> 리랜더링 -> console.log 출력 의 과정을 거치므로
4. console.log는 이벤트 발생 후 변경된 state를 출력하게 된다

라는 가정을 한 뒤, 코드로 실행해보았다.

```javascript
import React, { useState } from "react";
import "./App.css";

function Login() {
  const [email, setEmail] = useState("");

  const saveUserId = (event) => {
    setEmail(event.target.value);
  };

  console.log(email); // Component안에 console.log
  return (
    <div>
      <input
        type="text"
        placeholder="사용자 이메일"
        value={email}
        onChange={saveUserId}
      />
      <input type="password" placeholder="비밀번호" />
      <button>로그인</button>
    </div>
  );
}

export default Login;
```

<img src="/assets/images/20221204/reactrerander3.gif"/>
<br />
원하는 방식으로 console.log가 찍혔다!
<br />
가정했던 것이 맞았던 것 같다.
<br /><br /><br />
console.log를 찍다 리랜더링에 대해 다시 생각해보게 되었다. React를 다루면서 항상 `리랜더링`을 잊지말고 고려하도록 하자!
