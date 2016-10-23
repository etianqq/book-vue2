# 安装

####兼容性

Vue.js 不支持 IE8 及其以下版本，因为 Vue.js 使用了 IE8 不能实现的 ECMAScript 5 特性。 Vue.js 支持所有兼容 ECMAScript 5 的浏览器。

####NPM

在用 Vue.js 构建大型应用时推荐使用 NPM 安装， NPM 能很好地和诸如 Webpack 或 Browserify 模块打包器配合使用。 Vue.js 也提供配套工具来开发单文件组件。

    $ npm install vue
    
#####独立构建 vs 运行时构建

有两种构建方式，独立构建和运行构建。

1. 独立构建包括编译和支持 template 选项。 它也依赖于浏览器的接口的存在，所以你不能使用它来为服务器端渲染。

2. 运行时构建不包括模板编译，不支持 template 选项。运行时构建，可以用 render 选项，但它只在单文件组件中起作用，因为单文件组件的模板是在构建时预编译到 render 函数中，运行时构建只有独立构建大小的30%，只有 16Kb min+gzip大小。

默认 NPM 包导出的是 **运行时构建**。为了使用独立构建，在 webpack 配置中添加下面的别名：

    resolve: {
      alias: {
        'vue$': 'vue/dist/vue.js'
      }
    }