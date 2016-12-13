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




