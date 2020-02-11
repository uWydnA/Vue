# class与style

## 绑定HTML Class

### 对象语法

```html
<div id='box'>
    <div :class='classObj'>动态绑定ClassName</div>
</div>
```

```js
new Vue({
    el:'#box',
    data:{
        classObj:{
            aa:1,//true则显示该class名，false则不会
           	bb:0,
            cc:1
        }
    }
})
```



### 数组语法

```html
<div id='box'>
    <div :class='classArr'>动态绑定ClassName</div>
</div>
```

```js
new Vue({
	el:'#box',
    data:{
        classArr:['aa','cc']//数组里有的都会显示为className
    }
})
```



## 绑定内联样式

### 对象语法

```html
<div id='box'>
    <div :style='styleObj'>动态修改样式</div>
</div>
```

```js
new Vue({
	el:'#box',
    data:{
        styleObj:{
            backgroundColor:'#14c145'
        }
        //注意，直接用this.styleObj.属性=val，是无法渲染页面的，必须要使用
        // Vue.set(this.styleObj,属性,val)才可以渲染页面
    }
})
```

### 数组语法

```html
<div id='box'>
    <div :class='styleArr'>动态修改样式</div>
</div>
```

```js
new Vue({
	el:'#box',
    data:{
        styleArr:[{
            backgroundColor:"#14c145",
            fontSize:'12px'
        }]//注意，往数组中push对象，可以渲染页面
        //this.styleArr.push({color:'red'})
    }
})
```