# 리액트의 기본 구조

## 이 글은 21. 01. 10, 노마드 코더에서 시작한 Movie Services Clone Coding으로부터 출발합니다.

### 새로 안 사실

---

1. jsx function안에서 텍스트를 그냥 작성하면 HTML 텍스트가 되고,(HTML의 기본 구조와 같을 것이다.) **{} 안에 넣으면 자바스크립트**가 된다.
2. 리액트의 jsx에서는 class를 지정하기 위해 **className=""**태그를 사용해야한다.
3. 라우터를 사용한다면 라우터를 베이스로 작업을 하게 되고, 라우터들 끼리 push로 연결해주게 된다. (아직 라우터를 사용할 줄 모르니 자세한 라우터 사용은 새로운 마크다운 문서를 통해 남기겠다.)
4. App.js(jsx파일로 바꾸어 작업한다. 즉 **App.jsx**에서 기본 작업을 시작하게 되는데, `function App() {};` 안에 데이터를 선언하고, 이후 `return()`안에 html을 작성하고 파일경로 './component/blah.jsx'에서 작업한 컴포넌트를 `<blah />;` 형태로 끌고온 뒤 사이에 데이터 값을 `key={index}`이런 식으로 넣어주면 된다. 구조를 보자면,

```jsx
import logo from "./logo.svg";
import "./App.css";
import List from "./component/List";

function App() {
  const data = [
    { title: "title - 1", text: "text-1" },
    { title: "title - 2", text: "text-2" },
    { title: "title - 3", text: "text-3" },
    { title: "title - 4", text: "text-4" },
    { title: "title - 5", text: "text-5" },
  ];
  return (
    <div className="App">
      <h1 className="title">Example of React</h1>
      <ul className="list-wrapper">
        {data.map((el, index) => {
          return <List key={index} title={el.title} text={el.text} />;
        })}
      </ul>
    </div>
  );
}

export default App;
```

- 컴포넌트를 사용하는 다른 방법에는 map이 있다. 순서는 아래와 같다.

  - function에서 컴포넌트를 return해주는 구문을 작성하고, jsx내에서 map으로 렌더링.
  - renderFood 인자에서 기능을 불러오고, foodILike 배열에 있는 요소들을 모두 dish로 받은 다음, dish의 요소를 쪼개어 key, name, picture 순으로 한다.
  - key가 없다면 react 안의 요소들이 모두 unique하지 않아 에러가 뜰 수 있다. 그럴 경우, `id={index}`를 인자에 추가해서 key값을 각각 넣어주도록 한다. (맵이기 때문에 가능한 기능!)

  ```jsx
      <!-- 컴포넌트를 리턴해주는 구문 -->
  function renderFood(dish){
      return <Food key={dish.id} name={dish.name} picture={dish.image} />}
  function App() {
  return (
      <div className="App">
      <!-- jsx 내에서 map으로 렌더링 -->
      {foodILike.map(renderFood)}
      </div>;
  }

  function App() {
  return (
      <div className="App">
      <!-- 이건 renderfood 함수를 따로 선언하지 않고 안에 그대로 풀어쓴 형태. -->
      {foodILike.map(dish =>(
          <Food key={dish.id} name={dish.name} picture={dish.image} />
      ))}
      </div>);
  }
  ```

  - 차라리 map보다, 위 방법이 더 나은 것 같다..^^

5. Prop-types를 통해 전달받은 props가 원하는 형태인지 확인하기. (타입스크립트를 사용한다면 굳이 확인하지 않아도 되는 방법이다!)  
   설치는 bash에서 `npm i prop-types`
   [(React) PropTypes 사용방법과 종류](https://jistol.github.io/frontend/2018/12/03/react-proptypes/)

6. React에서는 onClick을 갖고있기 때문에 function 안에 펑션 이름을 써주면 된다.

```jsx
   render(){
   return <div>
   <h1>The number is: {this.state.count}.</h1>
   <button onClick={this.add}>Add</button>
   <button onClick={this.minus}>Minus</button>
   </div>
   }
```

그러나, add()하면 페이지가 onLoad되자마자 즉시 실행하는 것이고, ()를 떼면 클릭 되었을 때 실행되는 것이다. 즉, `onClick={this.add()}`와, `onClick={this.add}`는 언제 실행되냐에 따라 다르니 주의하라는 것이다.
