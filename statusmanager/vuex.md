#Vuex

![](/assets/vuex.png)


Vuex的核心是store(仓库)，其是一个容器，包含着应用中大部分的**状态(state)**。
Vuex 和单纯的全局对象有以下两点不同：

* Vuex 的状态存储是响应式的。当 Vue 组件从 store 中读取状态的时候，若 store 中的状态发生变化，那么相应的组件也会相应地得到高效更新。

* 不能直接改变 store 中的状态。改变 store 中的状态的唯一途径就是显式地提交(commit) mutations。

####state
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
```

####moutations

####actions

####modules