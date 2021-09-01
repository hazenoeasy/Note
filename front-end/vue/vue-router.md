# 动态路由匹配
把某种模式匹配到的所有路由都映射到同一组件。
path: '/user/:id', component: User 
$route.params.id可以保存动态路由的参数值

路由参数改变时，原来的组件会复用，因为两个路由都渲染相同的组件，比起销毁再创建，复用更加高效。所以组件生命周期钩子不会再被调用

复用组件时，可以watch¥route对象，或者使用2.2引入的beforeRouteUpdate导航守卫

捕获所有路由，可以使用通配符
{
    path:'*'
}
使用时应该保证通配符路由放在最后面。

[高级匹配模式](https://github.com/pillarjs/path-to-regexp/tree/v1.7.0#parameters) ?

# 嵌套路由

组件可以嵌套自己的router-view
```
const User = {
  template: `
    <div class="user">
      <h2>User {{ $route.params.id }}</h2>
      <router-view></router-view>
    </div>
  `
}
```

需要再vuerouter中配置children
```
const router = new VueRouter({
  routes: [
    { path: '/user/:id', component: User,
      children: [
        {
          // 当 /user/:id/profile 匹配成功，
          // UserProfile 会被渲染在 User 的 <router-view> 中
          path: 'profile',
          component: UserProfile
        },
        {
          // 当 /user/:id/posts 匹配成功
          // UserPosts 会被渲染在 User 的 <router-view> 中
          path: 'posts',
          component: UserPosts
        }
      ]
    }
  ]
})
```

# 编程式路由

this.$router.push
```
router.push('home')

router.push({ path: 'home' })

router.push({ name: 'user', params: { userId: '123' }})

// 带查询参数，变成 /register?plan=private
router.push({ path: 'register', query: { plan: 'private' }})
```

如何提供了path  params会失效 
```
const userId = '123'
router.push({ name: 'user', params: { userId }}) // -> /user/123
router.push({ path: `/user/${userId}` }) // -> /user/123
// 这里的 params 不生效
router.push({ path: '/user', params: { userId }}) // -> /user
```
在2.2.0+ 中 可在router.push  router.replace中提供onComplete onAbort回掉作为参数,在相应状态调用
在3.1.0+中， router.push & router.replace将返回一个promise

**如果路由相同，只是阐述发生了改变，需要使用beforeRouteUpdate来响应变化**

router.replace跟push一样，但是会替换掉history

router.go(n)在history记录中向前或者向后腿多少步.

# 命名路由

有时候，通过一个名称来标识一个路由显得更方便一些，特别是在链接一个路由，或者是执行一些跳转的时候。你可以在创建 Router 实例的时候，在 routes 配置中给某个路由设置名称。
```
const router = new VueRouter({
  routes: [
    {
      path: '/user/:userId',
      name: 'user',
      component: User
    }
  ]
})
```
```
<router-link :to="{ name: 'user', params: { userId: 123 }}">User</router-link>
router.push({ name: 'user', params: { userId: 123 }})
```

# 命名视图

展示多个视图，而不是嵌套展示，这时可以有多个router-view 同时进行命名

嵌套视图...

# 重定向 别名
重定向

path:'/a'  redirect:'/b'

当访问/a时 会跳转到/b

别名

path:'/a' alias:'/b'

可访问/b时 url会保持为/b    


# 路由组件传参

使用$route耦合度太强

使用props将组件和路由解耦

```
const User = {
  template: '<div>User {{ $route.params.id }}</div>'
}
const router = new VueRouter({
  routes: [
    { path: '/user/:id', component: User }
  ]
})
```

通过 props 解耦

```
const User = {
  props: ['id'],
  template: '<div>User {{ id }}</div>'
}
const router = new VueRouter({
  routes: [
    { path: '/user/:id', component: User, props: true },

    // 对于包含命名视图的路由，你必须分别为每个命名视图添加 `props` 选项：
    {
      path: '/user/:id',
      components: { default: User, sidebar: Sidebar },
      props: { default: true, sidebar: false }
    }
  ]
})
```

# H5 History模式

```
const router = new VueRouter({
  mode: 'history',
  routes: [...]
})
```
需要后台配置支持

# 导航守卫
通过跳转或者取消的方式守卫导航。有多种机会植入路由导航。

全局前置守卫
```
const router = new VueRouter({ ... })

router.beforeEach((to, from, next) => {
  // ...
})
```
* to 目的路由

* from 当前路由

* next 跳转函数   
  * next() 进入管道的下一个钩子
  * next(false) 中断路由 
  * next('/') 
  * next(error)


全局解析守卫

router.beforeResolve 注册全局守卫。在导航被确认之前，同时在所有组件内守卫和异步路由组件被解析之后，解析守卫就被调用

全局后置钩子
```
router.afterEach((to, from) => {
  // ...
})
```

路由独享的守卫
```
const router = new VueRouter({
  routes: [
    {
      path: '/foo',
      component: Foo,
      beforeEnter: (to, from, next) => {
        // ...
      }
    }
  ]
})
```

组内的守卫
```
const Foo = {
  template: `...`,
  beforeRouteEnter (to, from, next) {
    // 在渲染该组件的对应路由被 confirm 前调用
    // 不！能！获取组件实例 `this`
    // 因为当守卫执行前，组件实例还没被创建
  },
  beforeRouteUpdate (to, from, next) {
    // 在当前路由改变，但是该组件被复用时调用
    // 举例来说，对于一个带有动态参数的路径 /foo/:id，在 /foo/1 和 /foo/2 之间跳转的时候，
    // 由于会渲染同样的 Foo 组件，因此组件实例会被复用。而这个钩子就会在这个情况下被调用。
    // 可以访问组件实例 `this`
  },
  beforeRouteLeave (to, from, next) {
    // 导航离开该组件的对应路由时调用
    // 可以访问组件实例 `this`
  }
}
```
完整的导航解析流程

1. 导航被触发。
2. 在失活的组件里调用 beforeRouteLeave 守卫。
3. 调用全局的 beforeEach 守卫。
4. 在重用的组件里调用 beforeRouteUpdate 守卫 (2.2+)。
5. 在路由配置里调用 beforeEnter。
6. 解析异步路由组件。
7. 在被激活的组件里调用 beforeRouteEnter。
8. 调用全局的 beforeResolve 守卫 (2.5+)。
9. 导航被确认。
10. 调用全局的 afterEach 钩子。
11. 触发 DOM 更新。
12. 调用 beforeRouteEnter 守卫中传给 next 的回调函数，创建好的组件实例会作为回调函数的参数传入。
    
# 路由元信息

# 过渡动效

# 数据获取

# 滚动行为

# 路由懒加载
