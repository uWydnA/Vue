# v-model通信



```html
<div id="box">
    <input type="text" v-model='mytxt'>
    <child :text='mytxt'></child>
    <childmodel v-model='mytxt'></childmodel>
</div>
```

```JS
Vue.component("childmodel", {
    template: `
            <div>
            	childmodel -- {{value}}
            	<qbutton>click</qbutton>
            </div>
`,
   props:['value']
})
Vue.component("child", {
    template: `
            <div>
            	child -- {{text}}
            	<button>click</button>
            </div>
`,
    props: ['text']
})
new Vue({
    el: '#box',
    data: {
        mytxt: ""
    }
})
```

