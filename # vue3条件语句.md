# vue3条件语句
## v-if
    <p v-if="seen">现在你看到我了</p>
    //v-if 指令将根据表达式 seen 的值( true 或 false )来决定是否插入 p 元素
    //内容可以包裹其他元素一起不见
当然还有v-else和v-else-if

    <div id="app">
        <div v-if="Math.random() > 0.5">随机数大于 0.5</div>
        <div v-else-if="内容你自己脑补"></div>
        <div v-else>随机数小于等于 0.5</div>
    </div>

    <script>
        Vue.createApp(app).mount('#app')
    </script>
## v-show
可以使用 v-show 指令来根据条件展示元素：
    
    <h1 v-show="ok">Hello!</h1>
    //直接返回Hello
