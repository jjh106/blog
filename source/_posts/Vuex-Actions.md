---
title: Vuex-Actions
date: 2017-08-23 18:23:29
tags:
  - Vue
  - Vuex
---

Actions는 컴포넌트 대신 commit을 수행해준다.

#### # 액션 등록

```javascript
// index.js

export const store = new Vuex.Store({
  state: {
    count: 0
  },
  getters: {
	trippleCount(state) {
		return state.count * 3;
	},
	stringCount(state) {
		return state.count + ' Clicks';
	}
  },
  mutations: {
    increaseCount(state, payload={amount:1}) {
      state.count += payload.amount;
    },
    decreaseCount(state, payload) {
      state.count -= payload.amount;
    }
  },
  actions: {
    increaseCount(context, payload) {
      context.commit('increaseCount', payload);
    },
    decreaseCount({commit}, payload) {
      commit('decreaseCount', payload);
    }
  }
})
```

> context는 state, getters, commit 모두에 접근 가능하다.
>
> 파라미터로 commit을 부여하면 바로 사용 가능하다.

------

#### # 디스패치 액션

```javascript
// Counter.vue

// 기존 코드
import {mapMutations} from 'vuex';
export default {
  name: 'Counter',
  methods: {
    ...mapMutations([
      'increaseCount',
      'decreaseCount'
    ])
  }
}

// 변경 코드
export default {
  name: 'Counter',
  methods: {
    increaseCount(payload) {
      this.$store.dispatch('increaseCount', payload);
    },
    decreaseCount(payload) {
      this.$store.dispatch('decreaseCount', payload);
    }
  }
}
```

------

#### # 비동기작업 수행

```javascript
// index.js

export const store = new Vuex.Store({
  state: {
    count: 0
  },
  getters: {
	trippleCount(state) {
		return state.count * 3;
	},
	stringCount(state) {
		return state.count + ' Clicks';
	}
  },
  mutations: {
    increaseCount(state, payload) {
      state.count += payload;
    },
    decreaseCount(state, payload) {
      state.count -= payload;
    }
  },
  actions: {
    // Sync
    increaseCount(context, payload) {
      context.commit('increaseCount', payload.amount);
    },
    decreaseCount({commit}, payload) {
      commit('decreaseCount', payload.amount);
    },
    // Async
    increaseAsyncCount({commit}, payload) {
      window.setTimeout(function() {
        commit('increaseCount', payload.amount);
      }, payload.duration);
    },
  	decreaseAsyncCount({commit}, payload) {
      window.setTimeout(function() {
      	commit('decreaseCount', payload.amount);
      }, payload.duration);
  	}
  }
})

// Counter.vue

// Async Action Buttons
<button
  type="button"
  class="button is-increase"
  aria-label="Increase"
  @click="increaseAsyncCount({amount: 10, duration: 500})">+</button>
<button
  type="button"
  class="button is-decrease"
  aria-label="Decrease"
  @click="decreaseAsyncCount({amount: 5, duration: 500})">-</button>
```