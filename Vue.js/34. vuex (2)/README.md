# vuex (2)

> Vue.js官方的狀態管理套件，本篇說明進階的**Mutations**用法及透過Dispatch **Actions**來引發Mutations

## Github

[vuejs/vuex](https://github.com/vuejs/vuex)

## Commit Mutations with Payload

在觸發Mutations可另外傳遞參數，也就是Payload。
例如下面程式碼中，我們可透過Payload決定這次`count`加上的值，或是預設加`1`；

> 通常會指定Payload為object

#### Vuex instance

```javascript
import Vue from 'vue';
import Vuex from 'vuex'
Vue.use(Vuex)

export const store = new Vuex.Store({
    state: {
      count: 0
    },
    mutations: {
      increment (state, payload) {
        if(payload) state.count += payload;
        else state.count++;
      },
      //...skip
    }
})
```

#### Usage

讓狀態裡的`count`直接加`10`:

```javascript
let amt = 10;
store.commit("increment", amt);
```


## Use mapMutations to commit mutations

透過[注入vuex store到所有子元件](https://github.com/KarateJB/eBooks/tree/master/Vue.js/33.%20vuex%20(1)#%E6%B3%A8%E5%85%A5vuex-store%E5%88%B0%E6%89%80%E6%9C%89%E5%AD%90%E5%85%83%E4%BB%B6)，我們可以以全域方式取得或操作vuex store: `this.$store.state.count`；

另可透過[mapMutations](https://vuex.vuejs.org/guide/mutations.html#committing-mutations-in-components)來對應自訂的方法名稱至Mutations:

```javascript
import { mapMutations } from "vuex";

var app = new Vue({
  el: '#app',
  methods: {
    ...mapMutations({
      add: "increment", // Map `this.add()` to `this.$store.commit('increment')`
      minus: "decrement", // Map `this.add()` to `this.$store.commit('decrement')`
      clear: "reset" // Map `this.add()` to `this.$store.commit('decrement')`
    })
  },
})
```

這時候就可以使用自訂方法名稱來commit Mutations:

```javascript
this.add(10); //10 is the optional payload
this.minus();
this.clear();
```

也可以直接使用Mutations的原名稱作為自訂方法名稱：

```javascriptmethods: {
methods: {
    ...mapMutations({
      "increment", // Map `this.increment()` to `this.$store.commit('increment')`
      "decrement", // Map `this.decrement()` to `this.$store.commit('decrement')`
      "reset" // Map `this.reset()` to `this.$store.commit('decrement')`
    })
}
```



