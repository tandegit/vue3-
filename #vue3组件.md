# vue3组件
## 组件描述
创建组件
    app.component（。。。。）
挂载应用时，该组件被用作渲染的起点

    const app = Vue.createApp({})
    app.component('component-name', {
        /* ... */
        })
    //component-name 为组件名，/* ... */ 部分为配置选项

    <div id="app">
        <component-name></component-name>
    </div>
    //若/* ... */是template: '<h1>自定义组件!</h1>'，则输出“自定义组件！”
    app.mount('#app')
+ ##### 自定义按键
在上面的基础修改下配置选项

    app.component('button-counter', {
        data() {
            return {
                count: 0
            }
        },
        template: `<button @click="count++">点了 {{ count }} 次！</button>`
    })
    //就可以自定义按钮的显示

PS：组件是可以复用的

## 局部组件
可以通过一个普通的 JavaScript 对象来定义组件：
这样的局部组件只能在实例中使用

    const ComponentA = {
    /* ... */
    }
    ..........

    //然后直接在components选项中定义你想要使用的组件
    const app = Vue.createApp({
        components: {
            'component-a': ComponentA,
            'component-b': ComponentB
        }
    })//对于 components 对象中的每个属性来说，其属性名就是自定义元素的名字（component-a、
    component-b），其属性值就是这个组件的选项对象（ComponentA、ComponentB）。

## Prop
子组件用来接受父组件传递过来的数据的一个自定义属性
说白了就是继承

    <site-name title="Run1"></site-namet>//Run1
    <site-name title="Run2"></site-namet>//Run2

    //父组件需要用props来传递给子组件
    app.component('site-name', {
        props: ['title'],
        template: `<h4>{{ title }}</h4>`
    })
    //一个组件默认可以拥有任意数量的 prop，任何值都可以传递给任何 prop。

## 动态 Prop
可以用 v-bind 动态绑定 props 的值到父组件的数据中。每当父组件的数据变化时，该变化也会传导给子组件：

    <site-info
    v-for="site in sites"
    :id="site.id"
    :title="site.title"
    ></site-info>//返回1-Google，2-.....

    const Site = {
        data() {
            return {
                sites: [
                    { id: 1, title: 'Google' },
                    { id: 2, title: 'Runoob' },
                    { id: 3, title: 'Taobao' }
                 ]
            }
        }
    }//局部组件
 
    const app = Vue.createApp(Site)
 
    app.component('site-info', {
        props: ['id','title'],
        template: `<h4>{{ id }} - {{ title }}</h4>`
    })
 
    app.mount('#app')
## Prop 验证
为了可以验证，可以为 props 中的值提供一个带有验证需求的对象，而不是一个字符串数组
    
    Vue.component('my-component', {
        props: {
            propA: Number,    // 基础的类型检查 (`null` 和 `undefined` 会通过任何类型验证)
            propB: [String, Number],    // 多个可能的类型
            propC: {
                type: String,   // 必填的字符串
                required: true
            },   
            propD: {
                type: Number,// 带有默认值的数字
                default: 100
            },

            // 带有默认值的对象
            propE: {
                type: Object,   // 对象或数组默认值必须从一个工厂函数获取
                default: function () {
                    return { message: 'hello' }
                }
            },

            // 自定义验证函数
            propF: {
                validator: function (value) {
                // 这个值必须匹配下列字符串中的一个
                    return ['success', 'warning', 'danger'].indexOf(value) !== -1
                }
            }
        }
    })
    //当 prop 验证失败的时候，(开发环境构建版本的) Vue 将会产生一个控制台的警告，type也可以自定义
 