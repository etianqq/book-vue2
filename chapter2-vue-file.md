# 单文件组件

####介绍
在很多Vue项目中，我们使用 ```Vue.component``` 来定义全局组件，紧接着用 ```new Vue({ el: '#container '})``` 在每个页面内指定一个容器元素。


文件扩展名为 ```.vue ```的 single-file components(单文件组件) 为以上所有问题提供了解决方法，并且还可以使用 Webpack 或 Browserify 等构建工具。
![](vue-file.png)


