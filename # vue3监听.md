# vue3监听v-on
简写是@
下面是用watch来实现计数器

    <button @click = "counter++" style = "font-size:25px;">点我</button>

    const app = {
        data() {
            return {
                counter: 1
            }
        }
    }
    vm = Vue.createApp(app).mount('#app')
    vm.$watch('counter', function(new, old) {
        alert('计数器值的变化 :' + old + ' 变为 ' + new + '!');//这个是回调函数
    });

    //当然啦，可以内嵌这样写
    data(){
        ...
    },
    watch:{
        .....自己脑补
    }