---
title: Vuex-State
date: 2017-08-16 23:40:01
tags: Vue, Vuex
---

### # Vuex 준비

*vuex를 사용하기 전 설치를 하고 설정 해준다.*

```
npm i -D vuex
```

> 위의 명령어 입력
>
> src폴더 내부에 store폴더 생성
>
> store폴더에 index.js파일 생성

```javascript
import Vue from 'vue';
import Vuex from 'vuex';

Vue.use(Vuex);

export const store = new Vuex.store({
  state: {
    count: 0
  }
});
```

> vue와 vuex를 불러와 vue를 이용해 vuex 사용을 설정한다.
>
> store라는 이름으로 내보낸다.
>
> 내부의 state에서는 count를 중앙에서 제어할 수 있도록 설정해준다.

```javascript
import Vue from 'vue';
import App from './App.vue';
import {store} from './store';

new Vue({
  el: '#app',
  store,
  render: h => h(app)
})
```

> main.js에서 store를 불러온다.
>
> store를 사용하도록 el 아래에 추가해준다.

------

### # 실습

*vuex를 사용해 기존의 실습 코드를 변경해보자.* 

```javascript
data () {
  return {
    count: 0
  }
}
```

> App.vue의 data는 지워준다 !

```javascript
// 변경 전
methods: {
  onUpdateCount(value) {
    this.count += value;
  }
}

// 변경 후
methods: {
  onUpdateCount(value) {
    this.$store.state.count += value;
  }
}
```

> 마찬가지로 App.vue의 onUpdateCount 메서드도 변경해준다.

```javascript
computed: {
  count() {
    return this.$store.state.count;
  }
}
```

> App.vue에 위의 코드를 추가시켜주면 count 값은 :count="count"를 통해 Print.vue로 전달된다.
>
> Print.vue에서는 전달받은 count값( props: ['count'] )을 view로 뿌려주게 된다.( { count } )

```vue
// 변경 전
<template>
  <div id="app">
    <img src="./assets/logo.png">
    <h1>Vuex: 상태 관리 패턴 라이브러리</h1>
	<hr>
	<app-counter @onUpdate="onUpdateCount($event)"></app-counter>
	<app-print :count="count"></app-print>
  </div>
</template>

// 변경 후
<template>
  <div>
    <img src="./assets/logo.png">
    <h1>Vuex: 상태 관리 패턴 라이브러리</h1>
	<hr>
	<app-counter></app-counter>
	<app-print></app-print>
  </div>      
</template>
```

>  Vuex가 각각의 데이터를 자신의 컴포넌트에서 관리할 수 있기 때문에 App.vue의 템플릿을 수정해준다
>
> 위에서 작성한 methods와 computed 또한 필요없다!.......
>
> App.vue에는 컴포넌트 설정만 남겨둔다.

```javascript
// 변경 전
methods: {
  onIncrease() {
    this.$emit('onUpdate', 1);
  },
  onDecrease() {
    this.$emit('onUpdate', -1);
  }
}

// 변경 후
methods: {
  onIncrease() {
    this.$store.state.count++;  
  },
  onDecrease() {
    this.$store.state.count--;
  }
}
```

> Count.vue의 methods를 변경해준다.
>
> 부모의 종속관계에 상관없이 store객체에 바로 접근하여 count를 사용할 수 있기 때문에 코드 변경이 가능.

```javascript
// 변경 전
export default {
  name: 'Print',
  props: ['count']
}

// 변경 후
export default {
  name: 'Print',
  computed: {
    count() {
      return this.$store.state.count;  
    }
  }
}
```

> Print.vue에서도 count값을 props를 통해 받는 것이 아니고 computed를 통해 count를 리턴한다.