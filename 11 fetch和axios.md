# fetch&axios

XMLHttpRequest 是一个设计粗糙的 API，配置和调用方式非常混乱 ，基于事件的异步模型写起来不友好且兼容性不好。

因此我们可以学习去使用fetch&axios。

## fetch

[Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API) 提供了一个 JavaScript接口，用于访问和操纵HTTP管道的部分，例如请求和响应。它还提供了一个全局 [`fetch()`](https://developer.mozilla.org/zh-CN/docs/Web/API/GlobalFetch/fetch)方法，该方法提供了一种简单，合理的方式来跨网络异步获取资源。

这种功能以前是使用  [`XMLHttpRequest`](https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest)实现的。Fetch提供了一个更好的替代方法，可以很容易地被其他技术使用，例如 `Service Workers`。Fetch还提供了单个逻辑位置来定义其他HTTP相关概念，例如CORS和HTTP的扩展。

请注意，`fetch`规范与`jQuery.ajax()`主要有三种方式的不同，牢记：

- 当接收到一个代表错误的 HTTP 状态码时，从 `fetch()`返回的 Promise **不会被标记为 reject，** 即使该 HTTP 响应的状态码是 404 或 500。相反，它会将 Promise 状态标记为 resolve （但是会将 resolve 的返回值的 `ok` 属性设置为 false ），仅当网络故障时或请求被阻止时，才会标记为 reject。
- `fetch()` **不会接受跨域 cookies；**你也不能使用`fetch()` 建立起跨域会话。其他网站的`Set-Cookie`头部字段将会被无视。
- `fetch` **不会发送 cookies**。除非你使用了*credentials*的 [初始化选项](https://developer.mozilla.org/zh-CN/docs/Web/API/WindowOrWorkerGlobalScope/fetch#Parameters)。（自2017年8月25日以后，默认的credentials政策变更为`same-origin`。Firefox也在61.0b13版本中，对默认值进行修改）
- 

### get方式

一个基本的 fetch请求设置起来很简单。看看下面的代码：

```js
fetch('http://example.com/movies.json').then(response=>response.json()).then(function(myJson) {
    console.log(myJson);
});
```

这里我们通过网络获取一个JSON文件并将其打印到控制台。最简单的用法是只提供一个参数用来指明想`fetch()`到的资源路径，然后返回一个包含响应结果的promise(一个 [`Response`](https://developer.mozilla.org/zh-CN/docs/Web/API/Response) 对象)。

当然它只是一个 HTTP 响应，而不是真的JSON。为了获取JSON的内容，我们需要使用 [`json()`](https://developer.mozilla.org/zh-CN/docs/Web/API/Body/json)方法（在[`Body`](https://developer.mozilla.org/zh-CN/docs/Web/API/Body)mixin 中定义，被 [`Request`](https://developer.mozilla.org/zh-CN/docs/Web/API/Request) 和 [`Response`](https://developer.mozilla.org/zh-CN/docs/Web/API/Response) 对象实现）。



### post方式

1. form编码

```js
fetch('http://example.com/movies.json',{
    method:'post',
    headers:{
        'Content-Type':'application/x-www-form-urlencoded'
    },
    body:'name=retr0&age=1'
}).then(res=>res.json()).then(res=>{
    console.log(res)
})
```

2. json编码

```js
fetch('http://example.com/movies.json',{
    method:'post',
    headers:{
        'Content-Type':'application/json'
    },
    body:JSON.stringify({
        name:'retr0',
        age:12
    })
}).then(res=>res.json()).then(res=>{
    console.log(res);
})
```



## axios

### 安装

Using npm:

```
$ npm install axios
```

Using bower:

```
$ bower install axios
```

Using yarn:

```
$ yarn add axios
```

Using cdn:

```
<script src="https://unpkg.com/axios/dist/axios.min.js"></script>
```

### get方法

```js
axios.get('https://......').then(res=>{
    console.log(res.data) //数据在res.data中
})
```



### post方法

1. form编码

```js
axios.post('https://....','name=retr0&age=1').then(res=>{
    console.log(res.data)
})
```

2. json编码

```js
axios.post('https://...',{ //第二个参数直接传对象，不需要JSON.stringify()
    name:'retr0',
    age:1
}).then(res=>{
    console.log(res.data)
})
```



