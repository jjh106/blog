---
title: React-Mapping
date: 2017-06-30 00:14:45
tags: React
---

*Mapping은 다른 데이터를 지닌 배열을 묶어 Component 배열로 변환하여 효율적으로 렌더링해주는 것이다.* 

```javascript
class App extends React.Component {
  render() {
    return (
      <Contact/>
    );
  }
};

class Contact extends React.Component {
  render() {
    return (
      <ul>
        <li>Abet 010-0000-0001</li>
        <li>Betty 010-0000-0002</li>
        <li>Charlie 010-0000-0003</li>
        <li>David 010-0000-0004</li>
      </ul>
    );
  }
};
```

> 이름과 전화번호들이 반복된다. 이것들을 ContactInfo 컴포넌트로 묶어준다.

------

### # ContactInfo Component 만들기

```javascript
class ContactInfo extends React.Component {
  render() {
    return (
      <li>{this.props.name} {this.props.phone}</li>
    );
  }
};
```

> 이름과 전화번호가 나타날 부분에 props를 객체 형태로 받아와서 사용한다.

------

### # 기본 state 추가 및 ContactInfo Component 렌더링

```javascript
class Contact extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      contactData: [
        {name: 'Abet', phone: '010-0000-0001'},
        {name: 'Betty', phone: '010-0000-0002'},
        {name: 'Charlie', phone: '010-0000-0003'},
        {name: 'David', phone: '010-0000-0004'}
      ]
    };
  }
  render() {
    return (
      <ul>
        {this.state.contactData.map((contact, i) => {
          return (<ContactInfo name={contact.name}
                               phone={contact.phone}
                               key={i}/>);
        })}
      </ul>
    );
  }
};
```

> 상위 Component인 Contact에서 state를 설정해준다.
>
> 렌더링 부분을 Mapping로 변환.
>
> ContactInfo를 렌더링한다.

------

### # 최종 코드

```javascript
// App Component
class App extends React.Component {
  render() {
    return (
      <Contact/>
    );
  }
};
      
// Contact Component
class Contact extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      contactData: [
        {name: 'Abet', phone: '010-0000-0001'},
        {name: 'Betty', phone: '010-0000-0002'},
        {name: 'Charlie', phone: '010-0000-0003'},
        {name: 'David', phone: '010-0000-0004'}
      ]
    };
  }
  render() {
    return (
      <ul>
        {this.state.contactData.map((contact, i) => {
          return (<ContactInfo name={contact.name}
                               phone={contact.phone}
                               key={i}/>);
        })}
      </ul>
    );
  }
};

// ContactInfo Component
class ContactInfo extends React.Component {
  render() {
    return (
      <li>{this.props.name} {this.props.phone}</li>
    );
  }
};
```

------

### # Array.prototype.map

파라미터로 전달된 함수를 통해 배열 내의 각 요소를 프로세싱해 새로운 배열을 생성한다.

```javascript
var number = [1, 2, 3, 4, 5];

var doubled = number.map(num => num * 2);
```

> arr.map(callback, [thisArg])
>
> - callback : 새로운 배열의 요소를 생성하는 함수로 세 가지 인수를 가진다.
>   - currentValue : 현재 처리되고 있는 요소
>   - index : 현재 처리되고 있는 요소의 index값
>   - array : 메소드가 불려진 배열
> - thisArg : callback 함수 내부에서 사용할 this 값 설정.

------

*key에 대해서는 이해가 잘 가지 않아 좀 더 공부하고 기록해야겠다...*