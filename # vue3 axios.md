# vue3 axios
Vue 版本推荐使用 axios 来完成 ajax 请求。

Axios 是一个基于 Promise 的 HTTP 库，可以用在浏览器和 node.js 中。  

基础模板

    Vue.axios.get(api).then((response) => {
        console.log(response.data)
    })
## GET请求
常用response.data 读取 JSON 数据，这里只用respons

    <div>{{info}}</div>

    const app = {
    data() {
        return {
        info: 'Ajax 测试!!'  //这个是实际替换的内容
                            //get不到就是输出原内容
        }
    },
    mounted () {
        axios
        .get('https://www.runoob.com/try/ajax/json_demo.json')
        .then(response => (this.info = response))
        .catch(function (error) { // 请求失败处理
            console.log(error);
        });
    }
    }

#### GET 方法传递参数格式如下：
传递参数说明

    // 直接在 URL 上添加参数 ID=12345
    axios.get('/user?ID=12345')
    .then....
    .catch.....
    
    // 也可以通过 params 设置参数：
    axios.get('/user', {
        params: {
        ID: 12345
        }
    })
    .then....
    .catch.....
## POST方法
    new Vue({
        el: '#app',
        data () {
            return {
            info: null
            }
        },
        mounted () {
            axios
            .post('https://www.runoob.com/try/ajax/demo_axios_post.php')
            .then(response => (this.info = response))
            .catch(function (error) { // 请求失败处理
                console.log(error);
            });
        }
    })
#### POST 方法传递参数格式如下
    axios.post('/user', {
        firstName: 'Fred',        // 参数 firstName
        lastName: 'Flintstone'    // 参数 lastName
        })
        .then....
        .catch....
## 执行多个  并 发  请求
    function get1() {return axios.get('/user/12345');}
    function get2() {return axios.get('/user/12345/permissions');}

    axios.all([get1(), get2()])
        .then(axios.spread(function (acct, perms) {
        // 两个请求现在都执行完成
        }));
## axios API:可以直接在axios上进行请求
    axios(config)

    // 发送 POST 请求
    axios({
    method: 'post',
    url: '/user/12345',
    data: {
        firstName: 'Fred',
        lastName: 'Flintstone'
    }
    });

    //  GET 请求远程图片
    axios({
    method:'get',
    url:'http://bit.ly/2mTM3nY',
    responseType:'stream'
    })
    .then(function(response) {
    response.data.pipe(fs.createWriteStream('ada_lovelace.jpg'))
    });
    axios(url[, config])

    // 发送 GET 请求（默认的方法）
    axios('/user/12345');

## 创建实例

可以使用自定义配置.create新建一个 axios 实例：

    const instance = axios.create({
        baseURL: 'https://some-domain.com/api/',
        timeout: 1000,
        headers: {'X-Custom-Header': 'foobar'}
    });
#### 实例方法 
以下是可用的实例方法。指定的配置将与实例的配置合并：

    axios#request(config)
    axios#get(url[, config])
    axios#delete(url[, config])
    axios#head(url[, config])
    axios#post(url[, data[, config]])
    axios#put(url[, data[, config]])
    axios#patch(url[, data[, config]])
    //把#改成.就是请求的别名
## 部分请求配置项
    {
    // `url` 是用于请求的服务器 URL，这个必须有，其余可以省略
    url: "/user",

    // `method` 是创建请求时使用的方法
    method: "get", // 默认是 get，不写method就还是get

    // `baseURL` 将自动加在 `url` 前面，除非 `url` 是一个绝对 URL。
    // 它可以通过设置一个 `baseURL` 便于为 axios 实例的方法传递相对 URL
    baseURL: "https://some-domain.com/api/",

    // `transformRequest` 允许在向服务器发送前，修改请求数据
    // 只能用在 "PUT", "POST" 和 "PATCH" 这几个请求方法
    // 后面数组中的函数必须返回一个字符串，或 ArrayBuffer，或 Stream
    transformRequest: [function (data) {
        // 对 data 进行任意转换处理

        return data;
    }],
## 响应结构
axios请求的响应包含以下信息：

    {
    data: {},// `data` 由服务器提供的响应

    status: 200,// `status`  HTTP 状态码

    statusText: "OK",// `statusText` 来自服务器响应的 HTTP 状态信息
    
    headers: {},// `headers` 服务器响应的头

    config: {}// `config` 是为请求提供的配置信息
    }
使用 then 时，会接收下面这样的响应：

    axios.get("/user/12345")
    .then(function(response) {
        console.log(response.data);
        .......以此类推
        console.log(response.config);
    });
## 配置的默认值（全局）
可指定将被用在各个请求的配置默认值。

    axios.defaults.baseURL = '链接';
    axios.defaults.headers.common['Authorization'] = AUTH_TOKEN;
    axios.defaults.headers.post['Content-Type'] = '路径';
## 配置的优先顺序
先在 lib/defaults.js 找到的库的默认值，然后是实例的 defaults 属性，最后是请求的 config 参数。后者将优先于前者

    // 使用由库提供的配置的默认值来创建实例
    // 此时超时配置的默认值是 `0`
    var instance = axios.create();

    // 覆写库的超时默认值
    // 现在，在超时前，所有请求都会等待 2.5 秒
    instance.defaults.timeout = 2500;

    // 为已知需要花费很长时间的请求覆写超时设置
    instance.get('/longRequest', {
        timeout: 5000
    });
## 拦截器 interceptors
在请求或响应被then或catch处理前拦截

    //config可以是response
    //config是请求拦截器
    //response是响应拦截器
    axios.interceptors.request.use(function (config) {
        // 在发送请求之前做些什么/对响应数据做什么
        return config;
    }, function (error) {
        // 对请求/响应错误做些什么
        return Promise.reject(error);
    });
移除：.eject(...)

    axios.interceptors.request.eject(myInterceptor);
自定义：

    var instance = axios.create();
    instance.interceptors.request.use(function () {/*...*/});

## 取消执行
用 CancelToken.source 工厂方法创建 cancel token

    var CancelToken = axios.CancelToken;
    var source = CancelToken.source();

    axios.get('/user/12345', {
    cancelToken: source.token
    }).catch(function(thrown) {
    if (axios.isCancel(thrown)) {
        console.log('Request canceled', thrown.message);
    } else {
        // 处理错误
    }
    });

    // 取消请求（message 参数是可选的）
    source.cancel('Operation canceled by the user.');
还可以通过传递一个 executor 函数到 CancelToken 的构造函数来创建 cancel token：
    var CancelToken = axios.CancelToken;
    var cancel;

    axios.get('/user/12345', {
    cancelToken: new CancelToken(function executor(c) {
        // executor 函数接收一个 cancel 函数作为参数
        cancel = c;
    })
    });

    // 取消请求
    cancel();
    //可以使用同一个 cancel token 取消多个请求