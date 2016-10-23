# VUE2.0

[[中文文档](http://vuefe.cn/guide/)][[英文文档](http://vuejs.org/guide/)]
####Vue.js 是什么

Vue.js（读音 /vjuː/, 类似于 view） 是一套构建用户界面的 渐进式框架。与其他重量级不同的是，Vue 采用自底向上增量开发的设计。

从技术角度讲，Vue.js 专注于 MVVM 模型的 ViewModel 层。它通过双向数据绑定把 View 层和 Model 层连接了起来。实际的 DOM 封装和输出格式都被抽象为了 Directives 和 Filters。

Vue 的核心库只关注视图层，并且非常容易学习，非常容易与其它库或已有项目整合。另一方面，Vue 完全有能力驱动采用单文件组件和Vue生态系统支持的库开发的复杂单页应用。

Vue.js 的目标是通过尽可能简单的 API 实现响应的数据绑定和组合的视图组件。

![](vue-model.png)
####用组件构建（应用）

组件系统是 Vue.js 另一个重要概念，因为它提供了一种抽象，让我们可以用独立可复用的小组件来构建大型应用。如果我们考虑到这点，几乎任意类型的应用的界面都可以抽象为一个组件树：
![](vue-components.png)

在 Vue 里，一个组件实质上是一个拥有预定义选项的一个 Vue 实例：

    Vue.component('todo', {
      template: '<li>This is a todo</li>'
    })

现在你可以另一个组件模板中写入它：

    <ul>
      <todo-item></todo-item>
    </ul>
但是这样会为每个 todo 渲染同样的文本。

