---
title: Vuex-getters
date: 2017-08-17 21:42:55
tags: 
  - Vue
  - Vuex
---

### # PrintAnother 생성

새로운 vue 파일을 생성한다. (PrintAnother.vue)

```vue
<template>
  <div class="app-print">Another Print: {{ count }}</div>  
</template>

<script>
  export default {
    name: 'PrintAnother',
    computed: {
      count() {
        return this.$store.state.count;
      }
    }
  }
</script>
```

```javascript
this.$store.state.count * 3;
```

> Print.vue와 PrintAnother의 return값에 3을 곱하고 싶다.
>
>  이럴 경우 컴포넌트마다 수식을 붙여 줘야 하므로 복잡해지게 된다.
>
> 이것을 해결하기 위해서는 index.js에서 getters를 사용해야 한다.

------

### # getters 사용

getters는 state 내의 값을 사용자가 직접 접근하는 것이 아니고 getters를 통해 접근 가능하도록 해준다.

```javascript
export const store = new Vuex.Store({
  state: {
    count: 0
  },
  // getters
  getters: {
    trippleCount(state) {
      return state.count * 3;
    }
  }
});
```

> getters에 trippleCount 메서드를 생성.



```javascript
// 변경 전
{{ count }}

computed: {
  count() {
    return this.$store.state.count * 3;
  }
}

// 변경 후
{{ trippleCount }}

computed: {
  trippleCount() {
    return this.$store.getters.trippleCount;
  }
}
```

> 기존 computed의 count를 위 코드처럼 변경해준다! 



```javascript
// Print.vue
{{ stringCount }}

computed: {
  stringCount() {
    return this.$store.getters.stringCount;
  }
}

// index.js
getters: {
  stringCount(state) {
    return state.count + ' Clicks!!';
  }
}
```

> 한 번 더 연습하기 위해 stringCount를 만들어보자! 방법은 동일하다.



*프로젝트가 커질 경우 매번 return this.$store.getters.stringCount; 이런식으로 가져와 관리가 복잡해진다.*

*이 부분을 효율적으로 관리하기 위해서는 mapGetters를 사용한다.*

```javascript
import {mapGetters} from 'vuex';
export default {
  name: 'Print',
  computed: mapGetters([
    'trippleCount',
    'stringCount'
  ])
}
```

> 사용할 컴포넌트에서 mapGetters를 import해준다.
>
> computed 내부에 mapGetters를 사용한다.



```javascript
import {mapGetters} from 'vuex';
export default {
  name: 'Print',
  computed: mapGetters({
    tCount: 'trippleCount',
    sCount: 'stringCount'
  })
}
```

> 또한 해당 데이터를 받아올 때 다른 이름으로 사용할 수도 있다.(배열 대신에 객체로 변경)



```javascript
import {mapGetters} from 'vuex';
export default {
  name: 'Print',
  computed: {
    ...mapGetters({
      tCount: 'trippleCount',
      sCount: 'stringCount'
    })
  }
}
```

> 이전 코드처럼 computed에 직접적으로 mapGetters를 매핑하게 되면 다른 것들을 사용하기가 곤란하다.
>
> 그럴 경우 ...(spread parameter)를 사용한다.
>
> *문법을 올바르게 이해할 수 없다는 오류가 나오기 때문에 package.json에서 preset을 포함시켜줘야한다.

```
npm i -D babel-preset-stage-2
```

> 설치 완료!!!

```
{
  "presets": [
    ["env", { "modules": false }],
    ["stage-2"]
  ]
}
```

> *babelrc에 추가해준다!!