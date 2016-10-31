# 计算属性

建议，不要在模板中进行负责的数据计算，如果有这个需求，就利用```computed```-计算属性。

例子：
HTML

    <div id="example">
      <p>Original message: "{{ message }}"</p>
      <p>Computed reversed message: "{{ reversedMessage }}"</p>
    </div>

JS

    var vm = new Vue({
      el: '#example',
      data: {
        message: 'Hello'
      },
      computed: {
        // a computed getter
        reversedMessage: function () {
          // `this` points to the vm instance
          return this.message.split('').reverse().join('')
        }
      }
    })