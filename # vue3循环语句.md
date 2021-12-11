# vue3循环语句
***
## v-for
    <ul>
    //v-for 指令需要以 site in sites 形式的特殊语法
    //sites 是源数据数组并且 site 是数组元素迭代的别名。
	    <template v-for="site in sites">
		    <li>{{ site.text }}</li>
		    <li>--------------</li>
	    </template>
	</ul>

    return {
      sites: [
        { text: 'Google' },
        { text: 'Runoob' },
        { text: 'Taobao' }
      ]
    }//最终结果是渲染出一个列表

    //其实完全可以写成 v-for="变量 in 源数据数组"
#### 还可以支持多个参数

    <li v-for="(site, index) in sites">
      {{ index }} -{{ site.text }}
    </li>
    //(value, key, index)要按值，键，索引值这个顺序
#### 迭代整数
    <li v-for="n in 10">
        {{ n }}
    </li>
    //值得注意的是这里的10可以是一个方法返 回的值




    