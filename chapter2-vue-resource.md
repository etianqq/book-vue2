# vue-resource\(2.0\)
[
官方文档](https://github.com/pagekit/vue-resource/blob/master/docs/http.md)

####vue-resource插件具有以下特点：

**1. 体积小**

vue-resource非常小巧，在压缩以后只有大约12KB，服务端启用gzip压缩后只有4.5KB大小，这远比jQuery的体积要小得多。

**2. 支持主流的浏览器**

和Vue.js一样，vue-resource除了不支持IE 9以下的浏览器，其他主流的浏览器都支持。

**3. 支持Promise**API和**URI Templates**

Promise是ES6的特性，Promise的中文含义为“先知”，Promise对象用于异步计算。  
URI Templates表示URI模板，有些类似于ASP.NET MVC的路由模板。

**4. 支持拦截器**

拦截器是全局的，拦截器可以在请求发送前和发送请求后做一些处理。  
拦截器在一些场景下会非常有用，比如请求发送前在headers中设置access\_token，或者在请求失败时，提供共通的处理方式。

#### 使用

文件引用
```
<script src="js/vue-resource.js"></script>
```
组件内使用：
```
import Vue from 'vue';
import VueRouter from 'vue-router';
Vue.use(VueResource);

```


