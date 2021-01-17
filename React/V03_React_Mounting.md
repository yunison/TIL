# React의 Component 외의 다른 것들

Mounting: Component의 탄생

- Component가 mount 될 때, component가 screen에 표시될 땨, component가 내 Website에 진입할 때 constructor()을 호출한다.

→ constructor() : react에서 온게 아니라, js에서 클래스를 만들 때 나옴

→ static getDerivedS... 잘 안씀

→ render()

- Code

  ```jsx
  import React from "react";

  class App extends React.Component {
    state = {
      count: 0,
    };
    add = () => {
      this.setState((current) => ({ count: current.count + 1 }));
    };
    minus = () => {
      this.setState((current) => ({ count: this.state.count - 1 }));
    };
    componentDidMount() {
      //리액트가 업로드되는 즉시 불러와짐. 제 1순위
      console.log("component rendered");
    }

    render() {
      console.log("I'm rendering");
      return (
        <div>
          <h1>The number is: {this.state.count}.</h1>
          <button onClick={this.add}>Add</button>
          <button onClick={this.minus}>Minus</button>
        </div>
      );
    }
  }

  export default App;
  ```

  여기에서

  I'm rendering

  Component rendered

  순으로 콘솔이 찍힌다.

Updating: 통상적인 업데이트 (내가 클릭해서 상태를 바꿀 때. 그 때가 업데이트이다)

- getDerivedStateFromProps()
- shouldComponentUpdate()
- render
- get......Sna..
- **componentDidUpdate()**
- Console. 결과

  I'm rendering
  App.js:14 component rendered
  App.js:22 I'm rendering
  App.js:18 I just updated
  App.js:22

Unmounting: Component의 죽음 (페이지를 바꿀 때 사용)

mount되자마자 isLoading 은 무조건 true이다.( isLoading: true)

```jsx
class App extends React.Component {
  state = {
    isLoading: true,
  };
  componentDidMount() {
    setTimeout(() => {
      this.setState({ isLoading: false });
    }, 6000);
  }

  //componentDidMount는 페이지가 로딩되자마자 즉시 실행되는 함수이다.
  //따라서 API에서 가져온 동적 Data를 이곳에 가져와 fetching 시킨다.
  render() {
    const { isLoading } = this.state;
    return <div>{isLoading ? "Loading" : "We are ready"}</div>;
    //만약 isLoading이 true면 -> Loading 을 출력하고, : not true면 We are ready를 출력한다.
  }
}
```

---

# JS에서 data를 fetch하는 방법

1. fetch()
2. axios() → 미리 npm i axios를 통해 인스톨 필요

#4 Fetching Movies from API

```jsx
import React from "react";
import axios from "axios";

class App extends React.Component {
  state = {
    isLoading: true,
    // 첫 로딩 후에는 무조건 isLoading : true이다.
    movies: [],
    //미래를 위해 미리 선언하는 것은 필수가 아니다. 하지만 좋은 습관이다!
  };

  getMovies = async () => {
    const movies = await axios.get("https://yts-proxy.now.sh/list_movies.json");
    // async - await 비동기함수. movies는 axios가 URL을 get할 때 까지 기다려라. async는 무조건 써줘야 한다.
    // 2번
  };
  componentDidMount() {
    this.getMovies();
    //getMovies를 실행시킨다. 1번
  }
  render() {
    const { isLoading } = this.state;
    return <div>{isLoading ? "Loading" : "We are ready"}</div>;
  }
}

export default App;
```

es6의 코드를 더 단순하게 짜는 방법

```jsx
getMovies = async () => {
  const movies = await axios.get("https://yts-proxy.now.sh/list_movies.json");
  console.log(movies.data.data.movies);
};

getMovies = async () => {
  const {
    data: {
      data: { movies },
    },
  } = await axios.get("...");
  console.log(movies);
};
```
