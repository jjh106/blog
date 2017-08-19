---
title: Vuex-Mutations
date: 2017-08-19 23:51:43
tags:
  - Vue
  - Vuex
---

*store에 있는 state를 각 컴포넌트에서 임의로 수정하지 말고 Mutations를 이용하자.*

#### # Mutations 등록

```javascript
export const store = new Vuex.Store({
  state: {
    count: 0
  },
  getters: {
    trippleCount(state) {
      return state.count * 3;
    },
    stringCount(state) {
      return state.count + 'Clicks';
    }
  },
  mutations: {
    increaseCount(state) {
      state.count++;
    },
    decreaseCount(state) {
      state.count--;
    }
  }
});
```

> 기존 index.js에 mutations를 등록하자.

------

#### # Mutations 사용

```javascript
export default {
  name: 'Counter',
  methods: {
    onIncrease() {
      this.$store.commit('increaseCount');
    },
    onDecrease() {
      this.$store.commit('decreaseCount');
    }
  }
}
```

> Counter.vue에서 위의 코드처럼 commit를 이용해 사용하도록 한다.

------

#### # payload

```javascript
// index.js
mutations: {
  increaseCount(state, payload) {
    state.count += payload;
  },
  decreaseCount(state, payload) {
    state.count -= payload;
  }
}

// Counter.vue
onIncrease() {
  this.$store.commit('increaseCount', 2);
},
onDecrease() {
  this.$store.commit('decreaseCount', 1);
}

// 객체로 전달할 경우
state.count += payload.amount;
state.count -= payload.amount;

this.$store.commit('increaseCount', {amount: 2});
this.$store.commit('decreaseCount', {amount: 1});
```

> 첫 번째 전달인자 : 상태 값(state)
>
> 두 번째 전달인자 : payload 값
>
> index.js에서 payload 설정 후 사용할 때 전달인자를 추가한다. 위 코드에서는 2씩 증가, 1씩 감소되고 있다.
>
> payload는 객체로 전달도 가능하다.

------

#### # 다른 방법의 commit(객체 스타일 커밋)

```javascript
// Counter.vue
onIncrease() {
  this.$store.commit({
    type: 'increaseCount',
    amount: 2
  });
},
onDecrease() {
  this.$store.commit({
    type: 'decreaseCount',
    amount: 1
  });
}
```

------

#### # mapMutations

```javascript
// Counter.vue
import {mapMutations} from 'vuex';
export default {
  name: 'Counter',
  methods: {
    ...mapMutations({
      onIncrease: 'increaseCount',
      onDecrease: 'decreaseCount'
    })
  }
}

// index.js
mutations: {
  increaseCount(state, payload={amount: 1}) {
    state.count += payload.amount;
  },
  decreaseCount(state, payload={amount: 1}) {
    state.count -= payload.amount;
  }
}
```

> 컴포넌트 내부에서 변이를 커밋하고 싶을 때 사용
>
> payload에 초기 값을 위의 코드처럼 부여할 수도 있다.

##### amount 값을 전달하는 방식으로 사용하는 법

```vue
methods: {
  ...mapMutations([
    'increaseCount',
    'decreaseCount'
  ])
}

<button @click="increaseCount({amount: 10})"></button>
<button @click="decreaseCount({amount: 5})"></button>
```

> 배열로 매핑한다.
>
> 템플릿에서 적용!!