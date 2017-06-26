---
title: React-props
date: 2017-06-22 21:25:39
tags: React
---

*props는 component 내부의 변화하지 않는 데이터를 처리할 때 사용한다.*

```javascript
class Study extends React.Component {
  render() {
    return (
      <div>
        <h1>안녕 {this.props.name}</h1>
        <div>{this.props.children}</div>
      </div>		
    );
  }
}
class App extends React.Component {
  render() {
    return (
      <Study name="jjh">children이 나오게 되는 곳.</Study>
    );
  }
}
ReactDOM.render(<App/>, document.querySelector('#root'));
```

> Study component의 {this.props.name}은 상위 component인 App에서 설정(<Study name="jjh">) 해준다.
>
> 또한, {this.props.children}은 "children이 나오게 되는 곳." 텍스트가 위치한 곳에서 설정해 준다.

------

### # defaultProps

```javascript
class App extends React.Component {
  render() {
    return (
      <div>{this.props.value}</div>
    );
  }
};

App.defaultProps = {
  value: 0
};
```

> component 선언이 끝난 후 default객체를 설정한다.

------

### # propTypes

```javascript
class App extends React.Component {
  render() {
    return (
      <div>{this.props.value}</div>
    );
  }
};

App.propTypes = {
  name: React.propTypes.string,
  age: React.propTypes.number.isRequired
};

App.defaultPorps = {
  name: 'Unknown',
  age: 5
};
```

> props의 값이 특정 type이 아니거나 필수props를 입력하지 않았을 경우 경고를 띄울 수 있다.
>
> 마찬가지로 component 선언이 끝난 후 설정한다.
>
> name : 타입을 문자열로 설정
>
> age : 타입을 숫자로 설정하고 필수로 입력하게 한다.

------

*propTypes를 지정하는 것은 필수가 아니지만 유지 / 보수를 위해 설정하는 것이다.*

*다른 팀원이 내 component를 사용할 경우 해당 component가 어떤 props를 필요로하고 그것이*

*어떤 type인지 쉽게 알게 하기 위해서 사용한다.*



### Refer

##### [propTypes](https://facebook.github.io/react/docs/components-and-props.html)

##### [velopert님의 props](https://velopert.com/921)