# 基础篇

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


