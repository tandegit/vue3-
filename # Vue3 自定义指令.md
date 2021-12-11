# Vue3 自定义指令
模板语法

    <p>页面载入时，input 元素自动获取焦点：</p>
    <input v-focus>//就是整个输入框边缘变色已达到专注得目的

    const app = Vue.createApp({})
    // 注册一个全局自定义指令 `v-focus`
    app.directive('focus', {
    // 当被绑定的元素挂载到 DOM 中时……
        mounted(el) {
            // 聚焦元素
            el.focus()
        }
    })
    app.mount('#....')
## 局部指令
在实例使用 directives 选项来注册局部指令，这样指令只能在这个实例中使用：

    ......
    data(...),
    directives: {
      focus: {
         // 指令的定义
         mounted(el) {
            el.focus()
         }
      }
    }
# 钩子函数
指令定义函数提供了几个钩子函数（可选）

    app.directive('指令名', {
    // 指令是具有一组生命周期的钩子：
    
    created() {},  // 在绑定元素的 attribute 或事件监听器被应用之前调用

    beforeMount() {}, // 在绑定元素的父组件挂载之前调用
    
    mounted() {}, // 绑定元素的父组件被挂载时调用
   
    beforeUpdate() {},    // 在包含组件的 VNode 更新之前调用

    updated() {},  // 在包含组件的 VNode 及其子组件的 VNode 更新之后调用
    beforeUnmount() {},// 在绑定元素的父组件卸载之前调用
    
    unmounted() {} // 卸载绑定元素的父组件时调用
    })
    
    // 注册 (功能指令)
    app.directive('my-directive', () => {
    // 这将被作为 `mounted` 和 `updated` 调用
    })
    
    // getter, 如果已注册，则返回指令定义
    const myDirective = app.directive('my-directive')
# 钩子函数参数：el
el指令：绑定到的元素。这可用于直接操作 DOM
   
binding对象：其属性
* instance：使用指令的组件实例。
* ivalue：传递给指令的值。例如，在 v-my-directive="1 + 1" 中，该值为 2。
* ioldValue：先前的值，仅在 beforeUpdate 和 updated 中可用。值是否已更改都可用。
* iarg：参数传递给指令 (如果有)。例如在 v-my-directive:foo 中，arg 为 "foo"。
* imodifiers：包含修饰符 (如果有) 的对象。例如在 v-my-directive.foo.bar 中，修饰符对象为 {foo: true，bar: true}。
* idir：一个对象，在注册指令时作为参数传递。例如，在以下指令中： 

        app.directive('focus', {
            mounted(el) {
                el.focus()
            }
        })//idir 就是‘focus’后面的{....}内容
---
vnode

作为 el 参数收到的真实 DOM 元素的蓝图。

### 实例

        <div id="app">
            <div v-runoob="{ name: '菜鸟教程', url: 'www.runoob.com' }"></div>
        </div>

        const app = Vue.createApp({})
        app.directive('runoob', (el, binding, vnode) => {
        console.log(binding.value.name) // => "菜鸟教程"
        console.log(binding.value.url) // => "www.runoob.com"
        var s = JSON.stringify
        el.innerHTML = s(binding.value)
        })
        app.mount('#app')
#### 简写
当我们不需要写钩子函数，只要函数参数时就可以简写成

    <div id="app">
        <div v-runoob="{ color: 'green', text: '菜鸟教程!' }">
        </div>
    </div>

    Vue.directive('runoob', function (el, binding) {
        // 设置指令的背景颜色
        el.style.backgroundColor = binding.value.color
    })

    //指令函数可接受所有合法的 JavaScript 表达式
    以下实例可以传入了 JavaScript 对象：
    new Vue({
        el: '#app'
    })