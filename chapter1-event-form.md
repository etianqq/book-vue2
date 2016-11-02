# 事件

用 ```v-on``` 指令监听 DOM 事件来触发JavaScript 代码

HTML:

    <div id="example-3">
      <button v-on:click="say('hi')">Say hi</button>
      <button v-on:click="say">Say what</button>
    </div>

JS:

    new Vue({
      el: '#example-3',
      methods: {
        say: function (message) {
          alert(message || 'hello world!')
        }
      }
    })

####事件修饰符

* stop  ==> event.preventDefault();
* prevent ===> event.stopPropagation()
* capture 添加事件侦听器时使用时间捕获模式
* self 只当事件在该元素本身（而不是子元素）触发时触发回调

    <a v-on:click.stop.prevent="doThat"></a>

####按键修饰符
在监听键盘事件时，我们经常需要监测常见的键值。 Vue 允许为 ```v-on``` 在监听键盘事件时添加按键修饰符:

* enter
* tab
* delete (捕获 “删除” 和 “退格” 键)
* esc
* space
* up
* down
* left
* right

    <input v-on:keyup.enter="submit">