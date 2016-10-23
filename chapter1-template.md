# 模板语法
###插值
####1.文本

    <span>Message: {{ msg }}</span>

可以使用Javascript表达式，但是，只能是单个表达式，例如：

    <span>{{ ok ? 'YES' : 'NO' }} </span>
    <span>{{ message.split('').reverse().join('') }}</span>

**一次性插值**：```v-once```

    <span v-once>This will never change: {{ msg }}</span>

####2.HTML

    <div v-html="rawHtml"></div>

####3.属性
    <div v-bind:id="dynamicId"></div>
    <button v-bind:disabled="someDynamicCondition">Button</button>
    
简写```:property=value```

    <div :id="dynamicId"></div>
    <button :disabled="someDynamicCondition">Button</button>
    
####过滤器
Vue.js 允许你自定义过滤器，被用作一些常见的文本格式化。过滤器应该被添加在 mustache 插值的尾部，由“管道符”指示：

    {{ message | capitalize }}
    ...
    new Vue({
      // ...
      filters: {
        capitalize: function (value) {
          if (!value) return ''
          value = value.toString()
          return value.charAt(0).toUpperCase() + value.slice(1)
        }
      }
    })

###指令
指令（Directives）是带有 v- 前缀的特殊属性。指令属性的值预期是单一 JavaScript 表达式（除了 v-for，之后再讨论）。指令的职责就是**当其表达式的值改变时相应地将某些行为应用到 DOM 上**。如：

    <p v-if="seen">Now you see me</p>
    <a v-on:click="doSomething">
    
###缩写
1. v-bind缩写：```<a v-bind:href="url"></a> ==> <a :href="url"></a>```
2. v-on缩写：```<a v-on:click="doSomething"></a> ==> <a @click="doSomething"></a>```