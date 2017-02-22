#Vuex

![](/assets/vuex.png)


Vuex的核心是store(仓库)，其是一个容器，包含着应用中大部分的**状态(state)**。
Vuex 和单纯的全局对象有以下两点不同：

* Vuex 的状态存储是响应式的。当 Vue 组件从 store 中读取状态的时候，若 store 中的状态发生变化，那么相应的组件也会相应地得到高效更新。

* 不能直接改变 store 中的状态。改变 store 中的状态的唯一途径就是显式地提交(commit) mutations。

####1.state
Vuex 使用 **单一状态树** —— 用一个对象就包含了全部的应用层级状态。至此它便作为一个『唯一数据源(SSOT)』而存在。

这也意味着，**每个应用将仅仅包含一个 store 实例**(可以利用modules把store细分)。

vue组件内调用：
```
this.$store.state.count
```

####getter
有时候我们需要从 store 中的 state 中派生出一些状态，例如对列表进行过滤并计数：
```
const store = new Vuex.Store({
  state: {
    todos: [
      { id: 1, text: '...', done: true },
      { id: 2, text: '...', done: false }
    ]
  },
  getters: {
    doneTodos: state => {
      return state.todos.filter(todo => todo.done)
    }
  }
})
组件内使用：
computed: {
  doneTodosCount () {
    return this.$store.getters.doneTodosCount
  }
}
```

####2.moutations
mutations 非常类似于事件：每个 mutation 都有一个字符串的 事件类型 (type) 和 一个 回调函数 (handler)。
**mutation 必须是同步函数**
```
mutations: {
  //payload就是额外的参数
  increment (state, payload) {
    state.count += payload.amount;
  }
}
组件内触发事件：
this.$store.commit('increment'，{amount: 10}); 或者
this.$store.commit({
  type: 'increment',
  amount: 10
})
```
####3.actions
与mutations不同之处：

* Action 提交的是 mutation，而不是直接变更状态。
* Action 可以包含任意异步操作。

```
actions: {
  incrementAsync ({ commit }) {
    setTimeout(() => {
      commit('increment')
    }, 1000)
  }
}
组件内触发事件：
store.dispatch('incrementAsync', { amount: 10}); // 以载荷形式分发
或者
store.dispatch({ // 以对象形式分发
  type: 'incrementAsync',
  amount: 10
})
```

####4.modules

使用单一状态树，导致应用的所有状态集中到一个很大的对象。但是，当应用变得很大时，store 对象会变得臃肿不堪。

为了解决以上问题，**Vuex 允许我们将 store 分割到模块（module）。每个模块拥有自己的 state、mutation、action、getters、**甚至是嵌套子模块——从上至下进行类似的分割：
```
const moduleA = {
  state: { ... },
  mutations: { ... },
  actions: { ... },
  getters: { ... }
}

const moduleB = {
  state: { ... },
  mutations: { ... },
  actions: { ... }
}

const store = new Vuex.Store({
  modules: {
    a: moduleA,
    b: moduleB
  }
})

store.state.a // -> moduleA 的状态
store.state.b // -> moduleB 的状态
```
对于模块内部的 action，```context.state``` 是局部状态，根节点的状态是 ```context.rootState```:
```
const moduleA = {
  // ...
  actions: {
    incrementIfOddOnRootSum ({ state, commit, rootState }) {
      if ((state.count + rootState.count) % 2 === 1) {
        commit('increment')
      }
    }
  }
}
```