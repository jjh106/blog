---
title: React-JSX
date: 2017-06-21 00:04:13
tags: React
---

*JSX란 HTML과 JavaScript가 같은 파일에 위치하게 해주는 React.JS에서 사용하는 문법이다.*

*Babel-loader를 이용해 XML과 같은 문법을 JavaScript로 변환을 해준다.*

### 1. JSX 사용

< JS >

```javascript
class Study extends React.Component {
  render() {
    return (
      <div>리액트를 공부하자!</div>		
    );
  }
}

class App extends React.Component {
  render() {
    return (
      <Study/>
    );
  }
}

ReactDOM.render(<App/>, document.querySelector('#root'));
```

< HTML >

```html
<div id="root"></div>	
```

> ReactDOM.render()는 JSX형태의 코드를 실제 페이지에 렌더링할 때 사용된다.
>
> 이 메소드의 첫 번째 인수는 우리가 렌더링 할 JSX코드(<App/>)이고, 
>
> 두 번째 인수는 컴포넌트를 렌더링 할 Element(<div id="root"></div>)이다.

------

### 2. JSX의 특징

#### 2-1. 모든 JSX코드는 최상위 Container Element 안에 포함 시켜야 한다.

```javascript
/* 에러 발생 */
render() {
  return (
    <h1>안녕</h1>
  	<p>날씨가 좋아요</p>
  );
}

/* 올바른 작성 */
render() {
  return (
  	<div>
      <h1>안녕</h1>
      <p>날씨가 좋아요</p>
    </div>
  );
}
```

#### 2-2. JSX 안에서 JavaScript를 표현할 때는 {}으로 wrapping한다.

```javascript
render() {
  let text = "리액트를 공부하자!";
  return (
  	<div>{text}</div>
  );
}
```

#### 2-3. JSX의 Inline style

```javascript
render() {
  let style = {
    color: 'yellow',
    backgroundColor: 'black'
  };
  
  return (
  	<div style={style}>안녕~</div>
  );
}
```

> style 설정 시 string 형식이 아닌 key가 camelCase인 객체를 사용한다.

```javascript
render() {
  return (
  	<div className='heading'>안녕~</div>
  );
}
```

> class 설정 시 예약어인 class가 아닌 className를 사용한다.

#### 2-4. 주석

```javascript
render() {
  return (
  	<div>
      {/* 나는 주석이야 */}
    </div>
  );
}
```

> React의 주석은 JavaScript의 주석과 동일하지만 2-1의 내용처럼 Container Element 안에 작성해야 한다.