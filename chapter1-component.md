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