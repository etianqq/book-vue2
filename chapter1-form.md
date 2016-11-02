# 表单

用 ```v-model``` 指令在表单控件元素上创建双向数据绑定。

对于单选按钮，勾选框及选择列表选项， ```v-model``` 绑定的 value 通常是静态字符串（对于勾选框是逻辑值）：

    <!-- 当选中时，`picked` 为字符串 "a" -->
    <input type="radio" v-model="picked" value="a">
    <!-- `toggle` 为 true 或 false -->
    <input type="checkbox" v-model="toggle">
    <!-- 当选中时，`selected` 为字符串 "abc" -->
    <select v-model="selected">
      <option value="abc">ABC</option>
    </select>

####修饰符

* lazy

在默认情况下， ```v-model``` 在 ```input``` 事件中同步输入框的值与数据，但你可以添加一个修饰符 ```lazy``` ，从而转变为在 ```change``` 事件中同步

* number

如果想自动将用户的输入值转为 ```Number``` 类型（如果原值的转换结果为 NaN 则返回原值），可以添加一个修饰符 ```number``` 给 ```v-model``` 来处理输入值

* trim

如果要自动过滤用户输入的首尾空格，可以添加 ```trim``` 修饰符到 ```v-model``` 上过滤输入