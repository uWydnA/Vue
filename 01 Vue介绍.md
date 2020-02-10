# Vue介绍

## 官方介绍 

Vue (读音 /vjuː/，类似于view) 是一套用于构建用户界面的渐进式框架。与其它大型框架不同的是，Vue 被设计为可以自底向上逐层应用。Vue 的核心库只关注视图层，不仅易于上手，还便于与第三方库或既有项目整合。另一方面，当与现代化的工具链以及各种支持类库结合使用时，Vue 也完全能够为复杂的单页应用提供驱动。

## 渐进式

框架做分层设计，每层都可选，不同层可以灵活接入其他方案。而当你都想用官方的实现时，会发现也早已准备好，各层之间包括配套工具都能比接入其他方案更便捷地协同工作。一个个放入,放多少就做多少。



## MV*模式（MVC/MVP/MVVM）

### MVC

### MVP

### MVVM



## 引入
### script标签引入

```html
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
```



### Vue cli

Vue 提供了一个官方的 CLI，为单页面应用 (SPA) 快速搭建繁杂的脚手架

```
npm install ‐g @vue/cli
```





## 数据绑定原理

当你把一个普通的 JavaScript 对象传入 Vue 实例作为 data 选项，Vue 将遍历此对象所有的属性，并使用Object.defineProperty把这些属性全部转为 getter/setter。Object.defineProperty 是 ES5 中一个无法 shim 的特性，这也就是 Vue 不支持 IE8 以及更低版本浏览器的原因。

每个组件实例都对应一个 watcher 实例，它会在组件渲染的过程中把“接触”过的数据属性记录为依赖。之后当依赖项的 setter 触发时，会通知watcher，从而使它关联的组件重新渲染。

### Object.defineProperty

> `Object.defineProperty()` 方法会直接在一个对象上定义一个新属性，或者修改一个对象的现有属性， 并返回这个对象。

#### 语法

```
Object.defineProperty(obj, prop, descriptor)
```

##### 参数

- **obj**

  要在其上定义属性的对象。

- **prop**

  要定义或修改的属性的名称。

- **descriptor**

  将被定义或修改的属性描述符。

##### 返回值

 被传递给函数的对象

> 在ES6中，由于 Symbol类型的特殊性，用Symbol类型的值来做对象的key与常规的定义或修改不同，而`Object.defineProperty` 是定义`key`为Symbol的属性的方法之一。

#### 实例

```js
let obj = {};
    Object.defineProperty(obj,"myname",{
        get(data){
            console.log("被访问" + data);
        },
        set(data){
            console.log("被修改" + data)
        }
    })
```

#### 注意

Vue3 的 变化Object.defineProperty有以下缺点。

1. 无法监听es6的Set、Map 变化；
2. 无法监听Class类型的数据；
3. 属性的新加或者删除也无法监听；
4. 数组元素的增加和删除也无法监听。

#### 兼容性

针对Object.defineProperty的缺点，`ES6 Proxy`都能够完美得解决，它唯一的缺点就是，`对IE不友好`,所以vue3在检测到如果是使用IE的情况下（没错，IE11都不支持Proxy），会`自动降级`为`Object.defineProperty`的数据监听系统。