# Vue3 事件处理
v-on 指令可以缩写为 @ 符号  
我们需要使用一个方法来调用 JavaScript 方法。  
v-on 可以接收一个定义的方法来调用

    <button @click="greet">点我</button>

    const app={
        ........
        methods: {
            greet(event) {
                alert('Hello ' + this.name + '!') 
                // `methods` 内部的 `this` 指向当前活动实例
                //name在上面return里定义
                
                if (event) {
                    alert(event.target.tagName)//弹出的内容：“button”
                }
                // `event` 是原生 DOM event，这里弹出根组件的名字button
            }
        }
    }Vue.createApp(app).mount('#app')

当然啦，可以直接内联方法

    <button @click="one($event),two($event)">点我</button>
    
     methods: {
        one(event) {
            alert("第一个事件处理器逻辑...")
        },
        two(event) {
            alert("第二个事件处理器逻辑...")
        }
    }//事件处理程序中可以有多个方法，这些方法由逗号运算符分隔
## 按键修饰符

Vue 允许为 v-on 在监听键盘事件时添加按键修饰符：

    <!-- 只有在 keyCode 是 13 时调用 vm.submit() -->
    <input @keyup.13="submit">
    <!-- 同上 -->
    <input @keyup.enter="submit">

## .exact 修饰符

.exact 修饰符允许你控制由精确的系统修饰符组合触发的事件。

    <!-- 即使 Alt 或 Shift 被一同按下时也会触发 -->
    <button @click.ctrl="onClick">A</button>

    <!-- 有且只有 Ctrl 被按下的时候才触发 -->
    <button @click.ctrl.exact="onCtrlClick">A</button>
