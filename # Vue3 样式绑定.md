# Vue3 样式绑定
## 动态绑定class属性
为 v-bind:class 设置一个对象，从而动态的切换 class

    //事先定义一个方块
    .active {
    width: 100px;
    height: 100px;
    background: green;
    }

    <div :class="{ 'active': isActive }"></div>
    <div :style="{ color: activeColor, fontSize: fontsize + 'px' }">菜鸟教程</div>
    //当然return可以加其他class和对应值，就像上面的：style那
    样给：class多加一个键（.类）值（比如那个isActive）对就行

    const app = {
        data() {
            return {
                isActive: true //改为false则不显示方块
                activeColor：red
                fontsize:30 //上面没有'px'的话要改这里为'30px'
            }
        }
    }
    
    //上面等同于<div class="active:true/false"></div>

当然还可以内联样式

    <div :style="{ color: activeColor, fontSize: fontSize + 'px' }">
    菜鸟教程</div> //下面的模板自己脑补

    //也可以只写个对象
     <div :style="styleObject">菜鸟教程</div>
   
    在下面return{}里写
    styleObject: {
                color: "red",
			    fontSize: "30px"
	}
## 多重值
    <div :style="{ display: ['-webkit-box', '-ms-flexbox', 'flex'] }"></div>
    //这样写只会渲染数组中最后一个被浏览器支持的值。在本例中，如果浏览器支持不带浏览器前缀的 flexbox，那么就只会渲染 display: flex。

## 组件上使用 class 属性
    <runoob class="classC classD"></runoob>

    应用.component('runoob', {
        template: '<h1 class="classA classB">I like runoob!</h1>'
    })

    //组件用class的话不会覆盖被定义的根元素的class，只会添加
    //上面的结果为<h1 class="classA classB classC classD">I like runoob!</h1>
如果组件component有多个根元素，就需要我们去定义谁该接受这个类，方法是用$attrs 组件属性

    <runoob class="classA"></runoob>

    ....
        template: `
        <p :class="$attrs.class">I like runoob!</p>
        <span>这是一个子组件</span>
    `
    ......
    //这样<p>就接受到classA，<span>就没有接受
    //PS：此时的template 中 ` 是反引号，不是单引号 '