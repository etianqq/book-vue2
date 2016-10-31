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

地方
