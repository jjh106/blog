---
title: Vuex-Start
date: 2017-08-14 22:33:34
tags:
  - Vue
  - Vuex
---

*vuex를 공부하자!*

*시작 전 뷰 인스턴스를 다시 알아보고 가자.*

### # Vue Instance

```javascript
new Vue({
  // State
  data() {
    return {
      count: 0
    }
  },
  // View
  template: `
    <div>{{ count }}</div>
  `,
  // Actions
  methods: {
    inc() {
      this.count ++
    }
  }
})
```

> Vue 생성자를 통해 생성된 객체(컴포넌트)는 상태(State)를 통해서 View를, Actions를 처리하여 상태변경을 수행하고 뷰를 업데이트한다.

---

#### * 상태관리는 왜 필요한가 why!?

공통의 상태를 공유하는 여러 컴포넌트가 있는 경우 단순함이 빠르게 저하된다. 

지나치게 중첩된 컴포넌트는 부모에서 전달되는 prop이 길어질 수 있고, 형제 컴포넌트에서는 작동되지 않는다.

------

### # Vuex

*애플리케이션 상태 관리 패턴 라이브러리로 애플리케이션을 구성하는 모든 컴포넌트가 참조 가능한 상태를 중앙에서 관리하는 저장소이다.*

> 스토어의 state는 컴포넌트가 접근 가능한 데이터를 가지고 있다.
>
> state에 바로 접근해서 수정하는 것은 권장하지 않는다.
>
> 값을 가져올 땐 Getters를 통해 return된 값을 가져와야 한다.
>
> 자식 컴포넌트에서 커밋을 수행하면 Mutations를 통해서 상태변경을 해준다.
>
> Mutations는 동기적 수행만 가능하기 때문에 서버에서 가져오는 비동기처리는 할 수 없다.
>
> 비동기 처리를 가능하게 해주는 것은 Actions!!
>
> 사용자에게 Dispatch(통보)를 받으면 백엔드에서 API를 받으면 비동기로 처리가 끝났을 때 커밋을 통해 Mutations를 바꾸고 Mutations는 Sync를 통해 State를 변경하고 return된 그 값을 Getters를 이용해 다른 컴포넌트가 공유하게 된다.

------

#### 스토어(Store, 데이터 기억 저장장치)패턴

*스토어 객체 내부에는 데이터(State)와 데이터를 관리하는 메서드(Actions)로 구성된다. 디버깅을 위한 debug속성 또한 가진다. 이러한 유형의 중앙 집중식 상태 관리는 어떤 유형의 변이가 발생하는지, 어떻게 유발 되는지를 쉽게 이해할 수 있다.*

```javascript
var store = {
  debug: true,
  state: {
    message: 'Hello!'
  },
  setMessageAction(newValue) {
    this.debug && console.log('setMessageAction triggered with', newValue)
    this.state.message = newValue
  },
  clearMessageAction() {
    this.debug && console.log('clearMessageAction triggered')
    this.state.message = ''
  }
}
```

```javascript
var vmA = new Vue({
  data: {
    privateState: {},
    sharedState: store.state
  }
})

var vmB = new Vue({
  data: {
    privateState: {},
    sharedState: store.state
  }
})
```

> 스토어 객체를 만들고 스토어의 state값(store.state)을 공유할 수 있는 state(sharedState)로 뷰 인스턴스의
>
> data값으로 가지게 한다.