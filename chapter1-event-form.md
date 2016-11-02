# 事件和表单

####事件

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

#####事件修饰符

* stop  ==> event.preventDefault();
* prevent ===> event.stopPropagation()
* capture
* self