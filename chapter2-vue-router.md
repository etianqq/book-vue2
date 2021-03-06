# Vue-router(2.0)

[中文文档](https://github.com/vuejs/vue-router/tree/dev/docs/zh-cn)

####初始化

    import VueRouter from 'vue-router';
    import routeConfig from './route-config';
    ...
    Vue.use(VueRouter);
    ...
    const router = new VueRouter({routes: routeConfig});
    new Vue({
        router,
        el: '#app',
        render: h => h(App)
    });

####配置route config文件

    import page1 from './components/page1.vue';
    import page2 from './components/page2.vue';
    import children1 from './components/children1.vue';
    import children2 from './components/children2.vue';
    ...
    export default [
        {
            path: '/page1',
            name: 'page1',
            component: page1
        },
        //嵌套路由
        {
            path: '/page2/:id',  //
            name: 'page2',
            component: page2,
            children: [
                //默认会显示children1页面
                {
                    path: '',
                    name: 'children1',
                    component: children1
                },
                //路径为'/page2/2/children2'
                {
                    path: 'children2',
                    name: 'children2',
                    component: children2
                }
            ]
        },
        //默认重定向到/page1
        {
            path: '*',
            redirect: {name:'page1'}
        }
    ]

####命名路由
在创建 Router 实例的时候，在 routes 配置中给某个路由设置名称。

    const router = new VueRouter({
      routes: [
        {
          path: '/user/:id',
          name: 'user',
          component: User
        }
      ]
    })

要链接到一个命名路由，可以给 router-link 的 to 属性传一个对象(**一定使用```:to```**)：

    <router-link :to="{ name: 'user', params: { id: 123 }}">User</router-link>

或者

    // app.id为变量
    <router-link :to="'/user/' + app.id">User</router-link>
     
####编程式的导航
| 声明式 | 编程式 |
| -- | -- |
| ```<router-link to="...">``` | ```router.push(...)``` |

该方法的参数可以是一个字符串路径，或者一个描述地址的对象。例如：

    // 字符串
    router.push('home')

    // 对象
    router.push({ path: 'home' })

    // 命名的路由
    router.push({ name: 'user', params: { userId: 123 }})

    // 带查询参数，变成 /register?plan=private
    router.push({ path: 'register', query: { plan: 'private' }})


如果是组件，可以用```this.$router```取到```router```对象。

####路由元信息
组件里面可以用```this.$route```取到路由的只读信息。