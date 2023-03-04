## React

### 목차

1. [React 동작 원리](#React-동작-원리)
2. [vscode 설치](#vscode-설치)
3. [npm 설치](#npm-설치)
4. [React 세팅](#React-세팅)
5. [컴포넌트 만들기](#컴포넌트-만들기)
6. [Props](#Props)
7. [Router](#Router)
8. [성능 관련 Hook](#성능-관련-Hook)
9. [마무리](#마무리)
   <hr>

## React 동작 원리

React는 순수 자바스크립트입니다. 실제로 브라우저가 이해할 수 있는 건 `html`, `css`, `js`뿐입니다.

react는 `react-dom`을 이용해 우리가 작성한 react코드를 바벨을 이용해 순수 자바스크립트로 변환해주고,
index.html파일을 만들어줍니다.

1. react로 개발
2. 웹에 띄울 때 개발한 걸 babel을 사용해 순수 html로 변환해줌
3. 사용자나 우리가 보는건 변환된 순수 html 파일

### 왜 리액트를 쓸까요

`DOM(Document Object Model)`은 HTML 문서의 프로그래밍 인터페이스입니다. DOM을 활용해서 텍스트파일인 HTML에 프로그래밍 언어가 접근할 수 있게 합니다.

웹 브라우저는 `DOM을 활용해 객체에 자바스크립트와 CSS를 적용합니다.`

그러나 DOM은 동적 UI에 최적화 되어있지 않습니다. 수 많은 동적 연산을 웹이 처리하게되면 CSS 연산을 다시하고, 페이지를 다시 그리고 하는 과정에서 시간이 많이 소모됩니다.
DOM을 사용하지 않는 방법은 없기에 React는 `Virtual DOM`을 사용해 최적화합니다.

리액트는 동적으로 데이터가 변화했을 때 직접적으로 DOM을 조작하는 것이 아니라 DOM의 사본이라고 할 수 있는 새로운 Virtual DOM을 생성합니다.
그리고 새로 생성된 Virtual DOM과 이전에 저장된 Virtual DOM을 비교해 변경된 부분의 DOM만을 변경합니다.
이 과정을 위 `react-dom`이 처리해줍니다.

## vscode 설치

window: https://crazykim2.tistory.com/748

mac: https://www.lainyzine.com/ko/article/how-to-install-visual-studio-code-on-macos/

## npm 설치

https://nodejs.org/ko/ 에서 LTS 버전으로 받아주세요.

## React 세팅

1. 아무 폴더 만들어서 vscode에서 열어줍니다.
2. 터미널을 열고 아래 명령어를 입력합니다.
```
npx create-react-app [프로젝트 이름]
// ex) npx create-react-app counter
```
그럼 아래 사진처럼 되어있겠죠?!

<img width="1511" alt="스크린샷 2023-03-04 오후 8 18 06" src="https://user-images.githubusercontent.com/72312559/222897017-244d4c01-9944-466d-b09c-91c05e14df06.png">

<br>
터미널에서

```
cd 프로젝트 이름
npm start
```
를 입력해보세요.

`localhost:3000` url로 연결하면 리액트 앱이 열렸습니다!
src폴더 안에서 `App.js`, `index.js`를 제외하고 모두 삭제해주세요.
두 파일은 아래 코드로 일단 작성해주세요.

```jsx
// App.js
function App() {
  return <div className="App"></div>;
}

export default App;
```

```jsx
// index.js
import React from "react";
import ReactDOM from "react-dom/client";
import App from "./App";

const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);
```

### index.js

가장 최상단에서 실행되는 파일입니다. `root로 연결해 react-dom으로 html을 변환해줍니다.`

### App.js

우리가 작성해야할 가장 최상단 루트 파일입니다. 밑에서 배울 router처리를 해당 파일에서 하고, 추후 배울 전역 상태 관리 라이브러리 Provider를 연결하기도 합니다.

## 컴포넌트 만들기

- `src/components` 폴더를 만들고, 안에 `Button.jsx`를 만들어봅시다.

<img width="1511" alt="스크린샷 2023-03-04 오후 8 52 16" src="https://user-images.githubusercontent.com/72312559/222899045-572e85a1-39f6-45c9-af69-c3ec3ffddaac.png">

해당 컴포넌트를 사용하려면 `import`해서 사용하면 됩니다.

<img width="1511" alt="스크린샷 2023-03-04 오후 8 29 38" src="https://user-images.githubusercontent.com/72312559/222897392-2ece88c1-a199-4fc4-a593-9c366a914a3e.png">

## Props

### props 넘기기

<img width="1511" alt="스크린샷 2023-03-04 오후 8 32 02" src="https://user-images.githubusercontent.com/72312559/222897527-ae3b1da5-7c24-453e-b81a-7a054358d69b.png">

<img width="1511" alt="스크린샷 2023-03-04 오후 8 53 19" src="https://user-images.githubusercontent.com/72312559/222899207-d4e03e27-cdf0-4352-a310-29829b6bf243.png">

```jsx
// isButton처럼 뒤에 값을 초기화해주는 게 없으면 boolean(true) 값이다.
<Button onClick={countUp} isButton />
```

`localhost:3000`에서 확인해보면 잘 동작하는 걸 확인할 수 있습니다.

### props 받는 방법

```jsx
const Button = ({ onClick }) => <button onClick={onClick}>count up</button>;
```

```jsx
const Button = (props) => <button onClick={props.onClick}>count up</button>;
```

```jsx
// props 기본값 지정
const Button = ({ onClick: () => {}}) => <button onClick={props.onClick}>count up</button>;
```

⛔️ 함수에 return이 없는 건 한줄이라 그렇습니다. 모든 함수는 return이 필요합니다.

```jsx
const Button = (props) => <button onClick={props.onClick}>count up</button>;

// 아래와 같음

const Button = (props) => {
  return <button onClick={props.onClick}>count up</button>;
};
```

## Router

Router는 페이지 이동입니다. 이동할 때 url도 당연히 변해야 새로고침해도 남아있고 하겠죠?!

프로젝트 터미널에서 아래 명령어를 입력해주세요.
페이지 router 관련 터미널입니다.

```
npm install react-router-dom
```

`src 내부에 pages 폴더`를 만들어봅시다.

안에 `Main.jsx`, `Goorm.jsx`, `Kakao.jsx`를 만들어봅시다. (컴포넌트는 무조건 첫 문자 대문자)

```jsx
// src/pages/Main.jsx
import React from "react";
import { Link } from "react-router-dom";

const Main = () => (
  <section>
    <h1>Main</h1>
    <span>메인 페이지 입니다.</span>
    <div>
      <Link to="/goorm">goorm</Link> | <Link to="/kakao">kakao</Link>
    </div>
  </section>
);

export default Main;
```

```jsx
// src/pages/Goorm.jsx
import React from "react";
import { Link } from "react-router-dom";

const Goorm = () => (
  <section>
    <h1>Goorm</h1>
    <span>구름 웹 스터디</span>
    <div>
      <Link to="/">main</Link>
    </div>
  </section>
);

export default Goorm;
```

```jsx
// src/pages/Kakao.jsx
import React from "react";
import { Link } from "react-router-dom";

const Kakao = () => (
  <section>
    <h1>Kakao</h1>
    <span>카카오다.</span>
    <div>
      <Link to="/">main</Link>
    </div>
  </section>
);

export default Kakao;
```

```jsx
// src/App.js
import React from "react";
import { BrowserRouter as Router, Route, Routes } from "react-router-dom";

import Main from "./pages/Main";
import Kakao from "./pages/Kakao";
import Goorm from "./pages/Goorm";

function App() {
  return (
    <Router>
      <Routes>
        <Route path="/" element={<Main />} />
        <Route path="/goorm" element={<Goorm />} />
        <Route path="/kakao" element={<Kakao />} />
      </Routes>
    </Router>
  );
}

export default App;
```

위 코드를 입력하고, `localhost:3000`에서 확인해보면 어떤 느낌인지 알 것 같습니다.

Router를 통해 path가 `/`일 땐 `Main`컴포넌트를 보여주고, `/goorm`일 땐 `Goorm` 컴포넌트를 보여주는 방식입니다.

```jsx
// /kakao 뒤에 아무거나 와도 해당 컴포넌트 보여줌
// 보통 고유값이 있는 것들에서 많이 사용함(상품별 디테일)
// ex) localhost:3000/kakao/dsajkdvjakjfsakl
<Route path="/kakao/:tid" element={<Kakao />} />
```

더 많은 속성들이 궁금하다면: https://reactrouter.com/en/main/route/route

## 성능 관련 Hook

### useMemo

react는`props`, `상태`가 바뀌면 리랜더링을 합니다.
이 부분에서 리랜더링이 필요없는 부분까지 랜더링이 되는데요.
성능 최적화를 위해 `연산된 특정 값`을 재사용하는 `useMemo hook`을 제공해줍니다.

https://playcode.io/react 에서 useMemo가 안되어 있는 아래 코드를 실행하고 input에 값을 입력해보세요.

계속 data를 연산하며 console.log가 뜨는 걸 확인할 수 있습니다.

```jsx
import React, { useState } from "react";

function getFilterData(data) {
  console.log("data...");
  return data.filter((data) => data > 0);
}

export function App(props) {
  const [input, setInput] = useState("");
  const data = [1, 2, 3, 4, 5];

  const onChange = (e) => {
    const { value } = e.target;
    setInput(value);
  };

  const dataList = getFilterData(data);

  return (
    <div>
      <input value={input} onChange={onChange} />
      <div>{dataList}</div>
    </div>
  );
}

// Log to console
console.log("Hello console");
```

useMemo를 사용하면 첫 렌더링 이후 값을 계속 재사용하는 걸 알 수 있습니다.

```jsx
import React, { useState, useMemo } from "react";

function getFilterData(data) {
  console.log("data...");
  return data.filter((data) => data > 0);
}

export function App(props) {
  const [input, setInput] = useState("");
  const data = [1, 2, 3, 4, 5];

  const onChange = (e) => {
    const { value } = e.target;
    setInput(value);
  };

  const dataList = useMemo(() => getFilterData(data), [data]);

  return (
    <div>
      <input value={input} onChange={onChange} />
      <div>{dataList}</div>
    </div>
  );
}

// Log to console
console.log("Hello console");
```

### useCallback

useCallback은 useMemo랑 비슷합니다.

해당 hook은 `함수를 재사용하는 hook`입니다.

사실 `props`, `상태`가 바뀌면서 랜더링 될 때마다 함수를 새로 생성하는 것이 메모리, CPU 리소스를 크게 차지하는 작업이 아니라 부하가 생길일은 없지만, 
한번 만든 함수를 필요할 때만 새로 만들고 재사용하는 것은 중요합니다.

```jsx
import React, { useState, useMemo, useCallback } from "react";

function getFilterData(data) {
  console.log("data...");
  return data.filter((data) => data > 0);
}

export function App(props) {
  const [input, setInput] = useState("");
  const data = [1, 2, 3, 4, 5];

  // 함수 안에서 사용하는 값들은 모두 dependancy배열 안에 넣기
  // 아래 같은 경우엔 input값과 관계가 있으므로 해당 값 넣기
  const onChange = useCallback(
    (e) => {
      const { value } = e.target;
      setInput(value);
    },
    [input]
  );

  const dataList = useMemo(() => getFilterData(data), [data]);

  return (
    <div>
      <input value={input} onChange={onChange} />
      <div>{dataList}</div>
    </div>
  );
}

// Log to console
console.log("Hello console");
```

## 마무리

다들 고생하셨습니다~!

다음 주엔 `로컬스토리지를 사용한 React Todolist 만들기`, `tailwind css`를 다뤄보겠습니다.

[스터디 노션 링크](https://www.notion.so/goorm/Web-Develop-Study-af0ebfe5264947a287ef7ca01b0a9504?pvs=4)
