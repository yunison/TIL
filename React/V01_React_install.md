# React Study

# 제 1장, 리액트 설치

**Module not found  
———————————————**  
 npm i (npm install)
npm start

- 리액트 설치

  ### Facebook이 제공하는 [create-react-app](https://github.com/facebook/create-react-app)

  1. Node.js 설치 (가능하면 *[최신버전](https://nodejs.org/en/)*으로)
  2. 터미널 (windows의 경우에는 git bash를 이용하면 편리)
  3. 코드 에디터 (개인취향, 마음에 드는 거 쓰세요)

  ## Create React App 사용하기

  1. **작업환경 폴더에 터미널 위치 → npx create-react-app hello 입력**

  - `yarn start` (npm start)
  - `yarn build` (npm run build)
  - `yarn test` (npm run test)
  - `yarn eject` (npm run eject)

  * 여기서 hello는 새로 진행하는 프로젝트의 폴더이름이 됩니다.

  2. **리액트 앱이 완성된 폴더로 터미널을 이동시켜 yarn start 입력**

  3. **리액트 개발을 용이하게 하기위한 개발자 도구→ [확장프로그램 다운](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=en-US)**

  4. **React와 SCSS를 함께 사용하려면,**

  - react-route 설치 → `npm install react-router-dom --save`
  - index.js에서 App.js 대신,  
     `ReactDOM.render(<Routes />, document.getElementByID("root"))`  
     로 변경

    5.**App.js 파일에서 routes 컴포넌트를 구현하는 파일명 또한 App.js → Routes.js로 변경. 아래는 App.js였던 것...**

  ```jsx
  import React from "react";
  import { BrowserRouter as Router, Route, Switch } from "react-router-dom";
  import Login from "./pages/Login";
  import Main from "./pages/Main";

  class Routes extends React.Component {
    render() {
      return (
        <Router>
          <Switch>
            <Route exact path="/" component={Login} />
            <Route exact path="/main" component={Main} />
          </Switch>
        </Router>
      );
    }
  }
  export default Routes;
  ```

  6. **여기까지 훌훌 날려버리시길...**

  ```jsx
  import React from "react";
  import ReactDOM from "react-dom";

  ReactDOM.render(<Routes />, document.getElementById("root"));
  ```

  7. **scss 설치**

  ```bash
  npm install node-sass
  ```
