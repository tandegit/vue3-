# Vue3 计算属性
关键词: computed
直接一点可以在{{}}里写
    
    <div id="app">
    {{ message.split('').reverse().join('') }}
    </div>
但这种写法不合正常开发逻辑，就跟css最好不要用内联样式一样
应该要建一个vm实例在里面写  computed: {}

    <div id="app">
        <p>原始字符串: {{ message }}</p>
        <p>计算后反转字符串: {{ reversedMessage }}</p>
    </div>

    const app = {
        data() {
            return {
                message: 'RUNOOB!!'
            }
        },
        computed: {
            // 计算属性的 getter    
            reversedMessage: function () {
            // `this` 指向 vm 实例（vm就是v-model，v-if，v-else这种）
            return this.message.split('').reverse().join('')
            }
        }
    }
 
    Vue.createApp(app).mount('#app')

## methods
    methods: {
        reversedMessage2: function () {
            return this.message.split('').reverse().join('')
        }
    }//替换computed做法
跟computed效果一样，但因为没有缓存而快很多。computed渲染的起点是发生依赖关系，有缓存机制
## computed的getter 还有setter
computed 属性默认只有 getter ，不过在需要时你也可以提供一个 setter

    var vm = new Vue({
        el: '#app',
        data: {
            name: 'Google',
            url: 'http://www.google.com'
        },
        computed: {
            site: {
            // getter
                get: function () {
                    return this.name + ' ' + this.url
                },
            // setter
                set: function (newValue) {
                    var names = newValue.split(' ')
                    this.name = names[0]
                    this.url = names[names.length - 1]
                }
            }
        }
    })

    
    vm.site = '菜鸟教程 http://www.runoob.com';
    // 调用 setter， vm.name 和 vm.url 也会被对应更新
    document.write('name: ' + vm.name);//菜鸟教程
    document.write('<br>');
    document.write('url: ' + vm.url);//http://www.runoob.com
