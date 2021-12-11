# vue3 模板语法
## 基本语法
    const app = {
        data() {
            return {
                ok: true,
                message: 'RUNOOB!!',
                id: 1
            }
        }      
    }
    Vue.createApp(app).mount('#app')
    //这个是挂载，最后的参数是填上面的html元素的id，
    这样就能挂载到指定的html元素上
    //这其实也是dom的应用
## 文本语法
    <p>{{ message }}</p>
    //这个就不用解释了
## v-html语法
这个是用来输出html代码的

    <p>使用双大括号的文本插值: {{ rawHtml }}</p>
    <p>使用 v-html 指令: <span v-html="rawHtml"></span></p>

    data{return{
    rawHtml: '<span style="color: red">这里会显示红色！</span>'
    //第一个{{}}只会输出rawhtml的内容，第二个v-html写法才可以输出rawhtml的效果

## 属性 值用v-bind指令
比如

    <div v-bind:id="'list-' + id">菜鸟教程</div>

## 表达式和指令
* 表达式在{{}}中表达，如{{var a=i}}，但只能三元表达式而不能写控制流（*其实就是里面不能在嵌套一个{}*）
* 指令则是带有 v- 前缀的特殊属性
 
        <p v-if="seen">现在你看到我了</p>
        //v-if是根据seen的值觉得是否显示，若把seen的值改成false，null，
        undefined，就不显示

## 参数
    <a v-bind:href="url">菜鸟教程</a>
    //在指令后面用：连接，这里是v-bind指令将该元素的href属性与表达式 url 
    的值绑定

## 修饰符
以半角句号 . 指明的特殊后缀
如

    <form v-on:submit.prevent="onSubmit"></form>
    
## 巧妙的用户输入
    <p>{{ message }}</p>
    <input v-model="message">
    //在 input 输入框中我们可以使用 v-model 指令来实现双向数据绑定
    //结果是两个都有输出

关于监听v-on<br>
v-model 指令用来在 input、select、textarea、checkbox、radio 等表单控件元素上创建双向数据绑定，根据表单上的值，自动更新绑定的元素的值。

    <p>{{ message }}</p>
    <button v-on:click="reverseMessage">反转字符串</button>

    methods: {
        reverseMessage() {
        this.message = this.message
            .split('')
            .reverse()
            .join('')
        }
    }//这个例子是点一下就反转
## 缩写
    <a v-bind:href="url"></a>
    <a :href="url"></a>
    //v-bind的缩写

    <a v-on:click="doSomething"></a>
    <a @click="doSomething"></a>
    //v-on的缩写