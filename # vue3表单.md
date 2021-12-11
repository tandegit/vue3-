# vue3表单 双向绑定
v-model 会忽略所有表单元素的 value、checked、selected 属性的初始值，使用的是 data 选项中声明初始值。

    <input v-model="message1" placeholder="编辑我……">
    <textarea v-model="message" placeholder="多行文本输入……"></textarea>
    //多行输入

    const app = {
        data() {
            return {
                message1: ''
            }
        }
    }Vue.createApp(app).mount(#id)
    ....
    //表单没输入之前，输入框内显示有“编辑我”
v-model本身后面应该接方法等属性，因但为v-model 在内部为不同的输入元素使用不同的属性并抛出不同的事件：

    text 和 textarea 元素使用 value 属性和 input 事件；
    checkbox 和 radio 使用 checked 属性和 change 事件；
    select 字段将 value 作为属性并将 change 作为事件。
## 复选框 体现双向的绝佳例子
复选框如果是一个为逻辑值，如果是多个则绑定到同一个数组
注意value

    <input type="checkbox" id="runoob" value="Runoob" v-model="checkedNames">
    <label for="runoob">Runoob</label>
    <input type="checkbox" id="google" value="Google" v-model="checkedNames">
    <label for="google">Google</label>
    <br>
    <span>选择的值为: {{ checkedNames }}</span>

    ......
    return {
        checkedNames: []
    }
    ........

    //弹出来的复选框，勾了就会把对应的Google绑定到checkedNames展示

* 单选框
  
        <input type="checkbox" id="checkbox" v-model="checked">
        <label for="checkbox">{{ checked }}</label>

        ........
        return {
            checked : false
        }
        ........
        //返回一个单选框，点一下切换true/false
## 下拉表 select列表
    <select v-model="selected" name="fruit">
        <option value="">选择一个网站</option>
        <option value="www.runoob.com">Runoob</option>
        <option value="www.google.com">Google</option>
    </select>

    <div id="output">选择的网站是: {{selected}}
    </div>

    new Vue({
        el: '#app',
        data: {
            selected: '' 
        }
    })//快速绑定写法（这种写法有问题？到时候还是得const app=自己定义）
另外一个例子
    
    //在上面的基础上
    <select ..... multiple>
    //就可以复选了
## v-for的双向实现
    <select v-model="selected">
        <option v-for="option in options" :value="option.value">
            {{ option.text }}
        </option>
    </select>
    <span>选择的是: {{ selected }}</span>

    ......
    return {
      selected: 'www.runoob.com',
      options: [
        { text: 'Runoob', value: 'www.runoob.com' },
        { text: 'Google', value: 'www.google.com' },
        { text: 'Taobao', value: 'www.taobao.com' }
      ]
    }
    ........
    //结果跟上面的下拉表差不多
## 值绑定
对于单选按钮，复选框及选择框的选项，v-model 绑定的值通常是静态字符串 (对于复选框也可以是布尔值)：

    <input type="radio" v-model="picked" value="a" />
    //当选中时，`picked` 为字符串 "a"

    //toggle` 为 true 或 false
    <input type="checkbox" v-model="toggle" />

    //当选中第一个选项时，`selected` 为字符串 "abc"
    <select v-model="selected">
        <option value="abc">ABC</option>
    </select>
* 用 v-bind 可以实现把值绑定到当前活动实例的一个动态属性
        
        <input type="checkbox" v-model="toggle" true-value="yes" false-value="no" />
        ...
        vm.toggle === 'yes' // 选中时
        vm.toggle === 'no'// 取消选中 