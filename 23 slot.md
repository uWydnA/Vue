# slot

- **Props**：

  - `name` - string，用于命名插槽。

- **Usage**：

  `` 元素作为组件模板之中的内容分发插槽。`` 元素自身将被替换。

  详细用法，请参考下面教程的链接。

- **参考**：[通过插槽分发内容](https://cn.vuejs.org/v2/guide/components.html#通过插槽分发内容)

## 实例

### slot='val'

```html
<div id='box'>
    <child>
        <div slot='a'>a</div>
        <div slot='b'>b</div>
        <div slot='c'>c</div>
    </child>
</div>
```

```js
Vue.component("child",{
    template:`
		<div>
			<slot name='a'></slot>
			<slot name='b'></slot>
			<slot name='c'></slot>
		</div>
	`,
})
```

### v-slot

```html
<div id='box'>
    <template v-slot:a></template>
    <template v-slot:b></template>
    <template v-slot:c></template>
</div>
```

```js
Vue.component("child",{
    template:`
		<div>
			<slot name='a'></slot>
			<slot name='b'></slot>
			<slot name='c'></slot>
		</div>
	`,
})
```



## slot抽屉效果

```html
<div id='box'>
    <child>
    	 <button @click='isshow=!isshow'>显示/隐藏</button>
    </child>
    <slidebar v-show='isshow'></slidebar>
</div>
```

```js
Vue.component('child',{
    template:`
		<div>
			<slot></slot>
		</div>
	`
})
Vue.component('slidebar',{
    template:`
		<ul>
			....
		</ul>
	`
})
new Vue({
	el:'@#box',
    data:{
        isshow:false
    }
})
```

