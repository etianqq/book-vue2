# 组件

有两种方式定义全局组件：

1. 单页面：component.vue
2. ```Vue.component('my-component', {//选项})```

如果仅仅在某个Vue实例中使用组件，可以局部注册：

```
new Vue({
  // ...
  components: {
    // <my-component> 将只在父模板可用
    'my-component': <div>A custom component!</div>'
  }
})
```
####1.data必须是函数
```
<div id="example-2">
  <simple-counter></simple-counter>
</div>
Vue.component('simple-counter', {
  template: '<button v-on:click="counter += 1">{{ counter }}</button>',
  data: function () { //必须是函数
    return { counter: 0 } 
  }
})
new Vue({
  el: '#example-2'
})
```

####2.父子组件通信
通常父子组件会是这样的关系：组件 A 在它的模版中使用了组件 B 。它们之间必然需要相互通信：父组件要给子组件传递数据，子组件需要将它内部发生的事情告知给父组件。

在 Vue.js 中，父子组件的关系可以总结为 props down, events up 。父组件通过 props 向下传递数据给子组件，子组件通过 events 给父组件发送消息。看看它们是怎么工作的。
![](/assets/props-events.png)

#####使用prop传递数据
```
Vue.component('child', {
  // 声明 props
  props: {
         message:{
            type: String,
            default: ''
         }},
  // 就像 data 一样，prop 可以用在模板内
  // 同样也可以在 vm 实例中像 “this.message” 这样使用
  template: '<span>{{ message }}</span>'
})
//usage
<child message="hello!"></child> 或者
<child v-bind:message="parentMsg"></child> 或者
<child :message="parentMsg"></child>
```

######(1)单向数据流
**prop 是单向绑定的：当父组件的属性变化时，将传导给子组件，但是不会反过来。**这是为了防止子组件无意修改了父组件的状态——这会让应用的数据流难以理解。

另外，每次父组件更新时，子组件的所有 prop 都会更新为最新值。这意味着你不应该在子组件内部改变 prop 。如果你这么做了，Vue 会在控制台给出警告。

通常有两种改变 prop 的情况：
* prop 作为初始值传入，子组件之后只是将它的初始值作为本地数据的初始值使用；
```
props: ['initialCounter'],
data: function () {
  return { counter: this.initialCounter }
}
```
* prop 作为需要被转变的原始值传入。
```
props: ['size'],
computed: {
  normalizedSize: function () {
        return this.size.trim().toLowerCase()
     }
}
```
######(2)prop验证
组件可以为 props 指定验证要求。如果未指定验证要求，Vue 会发出警告。当组件给其他人使用时这很有用。
```
Vue.component('example', {
  props: {
    // 基础类型检测 （`null` 意思是任何类型都可以）
    propA: Number,
    // 多种类型
    propB: [String, Number],
    // 必传且是字符串
    propC: {
      type: String,
      required: true
    },
    // 数字，有默认值
    propD: {
      type: Number,
      default: 100
    },
    // 数组／对象的默认值应当由一个工厂函数返回
    propE: {
      type: Object,
      default: function () {
        return { message: 'hello' }
      }
    },
    // 自定义验证函数
    propF: {
      validator: function (value) {
        return value > 10
      }
    }
  }
})
```

#####自定义事件



