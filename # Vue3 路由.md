# Vue3 路由
Vue 路由允许我们通过不同的 URL 访问不同的内容
## 组件举例
`<router-link>` 是一个组件，该组件用于设置一个导航链接，切换不同 HTML 内容。 to 属性为目标地址， 即要显示的内容。使得 Vue Router 可以在不重新加载页面的情况下更改 URL，处理 URL 的生成以及编码

    <h1>Hello App!</h1>
    <p>
        <!--使用 router-link 组件进行导航 -->
        <!--通过传递 `to` 来指定链接 -->
        <!--`<router-link>` 将呈现一个带有正确 `href` 属性的 `<a>` 标签-->
        <router-link to="/">Go to Home</router-link>
        <router-link to="/about">Go to About</router-link>
    </p>
    <!-- 路由出口 路由匹配到的组件将渲染在这里-->
        <router-view></router-view>
## <router-view>
router-view 将显示与 url 对应的组件

    <router-link to="/">Go to Home</router-link>
    <router-link to="/about">Go to About</router-link>

    <!-- 路由出口 -->
    <!-- 路由匹配到的组件将渲染在这里 -->
    <router-view></router-view>

    const Home = { template: '<div>Home</div>' }
    const About = { template: '<div>About</div>' }
    
    // 2. 定义一些路由
    // 每个路由都需要映射到一个组件。
    const routes = [
        { path: '/', component: Home },
        { path: '/about', component: About },
    ]
    
    // 3. 创建路由实例并传递 `routes` 配置
    // 可以输入更多配置
    const router = VueRouter.createRouter({
    // 4. 内部提供了 history 模式的实现。为了简单起见，我们在这里使用 hash 模式。
        history: VueRouter.createWebHashHistory(),
        routes, // `routes: routes` 的缩写
    })
    
    const app = Vue.createApp({})  // 5. 创建并挂载根实例
    
    app.use(router) //确保 _use_ 路由实例使整个应用支持路由
    
    app.mount('#app')
    
    // 应用启动后链接就会有下划线
## <router-link> 相关属性
to:表示目标路由的链接。 当被点击后，内部会立刻把 to 的值传到 router.push()，所以这个值可以是一个字符串或者是描述目标位置的对象。

    <!-- 字符串 -->
    <router-link to="home">Home</router-link>
    <!-- 渲染结果 -->
    <a href="home">Home</a>
    //可以加
* replace  
    设置 replace 属性的话，当点击时，会调用 router.replace() 而不是 router.push()，导航后不会留下 history 记录。

`<router-link :to="{ path: '/abc'}" replace></router-link>`
* append  
设置 append 属性后，则在当前 (相对) 路径前添加其路径。例如，我们从 /a 导航到一个相对路径 b，如果没有配置 append，则路径为 /b，如果配了，则为 /a/b

        <router-link :to="{ path: 'relative/path'}" append></router-link>
* tag  
有时候想要 `<router-link>` 渲染成某种标签，例如` <li>`于是我们使用 tag prop 类指定何种标签，同样它还是会监听点击，触发导航。

        <router-link to="/foo" tag="li">foo</router-link>
        <!-- 渲染结果 -->
        <li>foo</li>
* active-class  和  exact-active-class  
设置链接激活时使用的 CSS 类名  
配置当链接被精确匹配的时候应该激活的 class

        <router-link v-bind:to = "..." 
        active-class = "CSS类名">Router Link 1</router-link>
        <router-link v-bind:to = "{...}"
        exact-active-class = "CSS类名">Router Link 1</router-link>
* event  
声明可以用来触发导航的事件。可以是一个字符串或是一个包含字符串的数组。
`格式跟上面一样`