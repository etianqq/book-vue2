# 列表渲染

####v-for

可以用于数组或者对象。

* 数组: ```<li v-for="item in items">```
* 对象: ```<li v-for="value in object">```

####组件 和 v-for
HTML

    <div id="todo-list-example">
      <input
        v-model="newTodoText"
        v-on:keyup.enter="addNewTodo"
        placeholder="Add a todo"
      >
      <ul>
        <li
          is="todo-item"  //指向模板
          v-for="(todo, index) in todos"
          v-bind:title="todo"
          v-on:remove="todos.splice(index, 1)"
        ></li>
      </ul>
    </div>

JS

    Vue.component('todo-item', {
      template: '\
        <li>\
          {{ title }}\
          <button v-on:click="$emit(\'remove\')">X</button>\
        </li>\
      ',
      props: ['title']
    })
    new Vue({
      el: '#todo-list-example',
      data: {
        newTodoText: '',
        todos: [
          'Do the dishes',
          'Take out the trash',
          'Mow the lawn'
        ]
      },
      methods: {
        addNewTodo: function () {
          this.todos.push(this.newTodoText)
          this.newTodoText = ''
        }
      }
    })

####注意事项

由于 JavaScript 的限制， Vue 不能检测以下变动的数组：

1. 当你直接设置一个项的索引时，例如： ```vm.items[indexOfItem] = newValue```
2. 当你修改数组的长度时，例如： ```vm.items.length = newLength```

为了避免第一种情况，使用set或者splice：

    // Vue.set
    Vue.set(example1.items, indexOfItem, newValue)
    
    // Array.prototype.splice`
    example1.items.splice(indexOfItem, 1, newValue)
    
避免第二种情况，使用 splice：

    example1.items.splice(newLength)
