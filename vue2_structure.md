#Vue2.0服务端渲染

![](/assets/vue-sever-render.jpg)

Vue2.0同时支持服务端，服务端渲染支持流式渲染。

因为HTTP请求也是流式，Vue 的服务端渲染结果可以直接 pipe 到返回的请求里面。这样一来，就可以更早地在浏览器中呈现给用户内容，通过合理的缓存策略，可以有效地提升服务端渲染的性能。

一个服务端渲染的例子：

**static/app.js**
```
(function () { 'use strict'　 
var createApp = function () {　　
　　 return new Vue({　　　
　　　 template: '<div id="app"> \
　　　　　 {{msg}} \
　　　　　 <button @click="click">click</button>\
　　　　 </div>',　　
　　　 data: {　　
　　　　 msg: 0　　
　　　 },　　　
　　　 methods : {　　　
　　　　 click : function() {　
　　　　　 alert(this.msg);　　　
　　　　 }　　　
　　　 }　　
　　 })
　 }　 　 
  // 判断当前环境是服务端环境还是浏览器环境　
　 if (typeof module !== 'undefined' && module.exports) {　　
　　 // 服务端环境，返回实例的构造函数　
　　 module.exports = createApp
　 } else {　　
　　 // 浏览器环境，直接进行实例化　
　　 this.app = createApp()　
　 }
}).call(this)

```

**index.html**
```
<!DOCTYPE html>
<html>
<head>
　 <title>SSR</title>
　 <script src="http://cdn.bootcss.com/vue/2.0.3/vue.min.js"></script>
</head>
<body>
　 <div id="app"></div>　
　 <script src="/static/app.js"></script>　
　 <script>app.$mount('#app')</script>
</body>
</html>
```

**服务端代码 server.js**
```
'use strict'
var fs = require('fs')
var path = require('path')
global.Vue = require('vue')
// 获取index.html布局
var layout = fs.readFileSync('./index.html', 'utf8')
var renderer = require('vue-server-renderer').createRenderer()
// 创建一个Express服务器
var express = require('express')
var server = express()
// 设置"static"文件夹为静态资源路径
server.use('/static', express.static(　
　path.resolve(__dirname, 'static')
))
// 处理所有的Get请求
server.get('*', function (request, response) {　
　 renderer.renderToString(　　
　　 // 获取app.js的Vue实例　　 
    require('./static/app')(),　
　　 function (error, html) {　　
　　　 if (error) {　　　　
　　　　 console.error(error)　　　
　　　　 return response
　　　　　 .status(500)　　　
　　　　　 .send('Server Error')　　
　　　 }　　　
　　　 // 将渲染好的HTML插入替换index.html中，返回给浏览器　　
　　　 response.send(layout.replace('<div id="app"></div>', html))　
　　 }　
　 )
})
// 监听3000端口，通过http://localhost:3000/访问应用
server.listen(3000, function (error) {　
　 if (error) throw error
　 console.log('Server is running at localhost:5000')
})
```