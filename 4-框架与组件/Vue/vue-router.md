#### 背景

在开发提分加项目的过程中，遇到了点击下拉菜单时在新窗口中打开页面，由于之前一直做的是单页面应用，没有碰到过类似的需求，于是上网搜了一下解决办法，也再次系统地温习了一下`vue-router`。

#### 解决

使用路由对象的resolve方法解析路由，可以得到location、router、href等目标路由的信息。得到href就可以使用window.open开新窗口了。

```javascript
const {href} = this.$router.resolve({
    name: "statistics-explain",
    params: {
        classID: id,
        examSubjectID: this.planClassData.examSubjectID,
        studentStatus: 0
    }
});
window.open(href, '_blank');
```

> 参考文章：[vuerouter怎么点击打开新的页面，就是a标签里的target=“blank”](https://segmentfault.com/q/1010000009557100)

#### 延伸

> 参考文章：[Vue Router](https://router.vuejs.org/zh/)

- 动态路由匹配：一个“路径参数”使用冒号 `:` 标记。当匹配到一个路由时，参数值会被设置到 `this.$route.params`，可以在每个组件内使用。

- 嵌套路由：要在嵌套的出口中渲染组件，需要在 `VueRouter` 的参数中使用 `children` 配置，**要注意，以 / 开头的嵌套路径会被当作根路径。 这让你充分的使用嵌套组件而无须设置嵌套的路径。**

  ```javascript
  export default {
    path: '/scoreplus',
    name: 'scoreplus',
    component: { template: '<router-view />' },
    redirect: { name: 'scoreplus-index' },
    children: [
      {
        // 查看个人方案
        path: 'preview/:examSubjectID/:xuexinID/:recordsID/:constitute/:planID',
        name: 'score-preview',
        meta: { text: '个人方案' },
        component: ScorePreview
      },
      {
        // 查看方案内容
        path: 'planList/:planID',
        name: 'score-plan-list',
        meta: { text: '查看方案内容' },
        component: ScorePlanList
      },
      {
        // 下载方案内容
        path: 'download/:planID/:classID',
        name: 'score-download-list',
        meta: { text: '下载方案内容' },
        component: DownloadList
      },
      {
        // 查看推送试题
        path: 'push/:planID/:level',
        name: 'score-question-push',
        meta: { text: '查看推送试题' },
        component: QuestionPush
      },
      {
        // 提分方案首页
        path: '',
        name: 'scoreplus-index',
        component: ScoreIndex
      }
    ]
  }
  ```

- 编程式导航

  1. `router.push(location, onComplete?, onAbort?)`：想要导航到不同的 URL，则使用 `router.push` 方法。这个方法会向 history 栈添加一个新的记录，所以，当用户点击浏览器后退按钮时，则回到之前的 URL。

     ```javascript
     // 字符串
     router.push('home')
     // 对象
     router.push({ path: 'home' })
     // 命名的路由
     router.push({ name: 'user', params: { userId: 123 }})
     // 带查询参数，变成 /register?plan=private
     router.push({ path: 'register', query: { plan: 'private' }})
     ```

     在 2.2.0+，可选的在 `router.push` 或 `router.replace` 中提供 `onComplete` 和 `onAbort` 回调作为第二个和第三个参数。这些回调将会在导航成功完成 (在所有的异步钩子被解析之后) 或终止 (导航到相同的路由、或在当前导航完成之前导航到另一个不同的路由) 的时候进行相应的调用。

  2. `router.replace(location, onComplete?, onAbort?)`：跟 `router.push` 很像，唯一的不同就是，它不会向 history 添加新记录，而是跟它的方法名一样 —— 替换掉当前的 history 记录。

  3. `router.go(n)`：这个方法的参数是一个整数，意思是在 history 记录中向前或者后退多少步，类似 `window.history.go(n)`。

- 命名路由：可以在创建 Router 实例的时候，在 `routes` 配置中给某个路由设置名称。要链接到一个命名路由，可以给 `router-link` 的 `to` 属性传一个对象。

  ```vue
  <router-link :to="{ name: 'user', params: { userId: 123 }}">User</router-link>
  
  router.push({ name: 'user', params: { userId: 123 }})
  ```

- 重定向和别名

  1. 重定向（redirect）：

     ```javascript
     const router = new VueRouter({
       routes: [
         { path: '/a', redirect: '/b' }
       ]
     })
     ```

  2. 别名：**/a 的别名是 /b，意味着，当用户访问 /b 时，URL 会保持为 /b，但是路由匹配则为 /a，就像用户访问 /a 一样。**

     ```javascript
     const router = new VueRouter({
       routes: [
         { path: '/a', component: A, alias: '/b' }
       ]
     })
     ```

     