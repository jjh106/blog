---
title: React-state
date: 2017-06-26 21:02:29
tags: React
---

*state는 component에서 유동적인 데이터를 보여줄 때 사용된다.*

### # 사용 시 초기 값 설정이 필수이다.

```javascript
class Counter extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      value: 0
    };
  }
  render() {
    return (
      <div>
        <h2>{this.state.value}</h2>
        <button>Press Me</button>
      </div>
    )
  }
}
```

> 기본값 설정을 하지 않을 경우 렌더링{this.state.stateName} 시 에러가 난다.
>
> super를 통해 상속 받은 React.Component의 생성자 메소드를 먼저 실행하고 state나 props에 접근한다.

------

### # this.setState({...})로 컴포넌트 내부에서 값을 변경할 수 있다.

```javascript
class Counter extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      value: 0
    };
    this.handleClick = this.handleClick.bind(this);
  }
  
  handleClick() {
    this.setState({
      value: this.state.value + 1
    });
  }
  
  render() {
    return (
      <div>
        <h2>{this.state.value}</h2>
        <button onClick={this.handleClick}>Press Me</button>
      </div>
    )
  }
}
```

> ES6의 class에서는 auto binding이 되지 않기 때문에 setState 메소드를 사용할 이벤트를 바인딩 해줘야 함.
>
> render() 내부의 onClick={this.handleClick}에서 this가 무엇인지 모르기 때문에 자바스크립트 엔진은 최상위에 위치한 window를 연결한다. 그렇기 때문에 constructor 내부에서 직접 바인딩 시켜준다.(아직 정확히 이해하지 못함...)
>
> 이런 문제는 arrow function을 사용하면 this를 자동으로 바인딩 해주기 때문에 간단히 해결된다. 

------

*props와 달리 state는 그 컴포넌트 내부에서만 사용될 때 쓰는 것이 옳다. 만약 state값을 다른 컴포넌트에서* 

*접근 할 일이 생긴다면 부모 컴포넌트에서 state를 사용하고 그 값을 props로 자식 컴포넌트에 넘겨 받는 방식이*

*권장된다. React.js 어플리케이션을 만들 땐 state를 사용하는 컴포넌트의 갯수를 최소화 하자!*