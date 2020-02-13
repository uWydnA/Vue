## vue checkbox使用v-model和@click遇到的坑

### 1. 问题描述：

- 使用v`-model="value"`对checkbox进行了绑定，同时监听checkbox 的`click事件`，在click方法中使用了this.value取值。发现不同浏览器下，取到的this.value的值是`不同`的。

代码如下：

```
<template>
  <div class="hello">
    <input type="checkbox" v-model="checkboxValue" @click="onClick"/>
  </div>
</template>
<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      checkboxValue: false
    }
  }
  methods:{
    onClick(){
      console.log(this.checkboxValue);
    }
  }
}
```

 以上代码默认checkbox是未选中状态，value是false。
当点击Checkbox选中的时候，会进入onClick的方法中。
 发现不同浏览器读取的`this.checkboxValue`的值是不同的

```
Firefox / Chrome`
`打印输出： false`
`IE:`
`打印输出： true
```

 也就是说在`Firefox/Chrome`浏览器下，是先执行click方法，然后再对checkboxValue进行赋值。
 而在`IE`下，是先对checkboxValue进行赋值，然后在执行click方法。

### 2. 原因分析

 与v-model的语法糖有关，详情请看[《v-model语法糖》](http://jessyhong.github.io/2018/03/25/v-model-explain-detail/)

```
<input type="checkbox" v-model="sth" />
<input type="checkbox" :checked="checkboxValue" @change="checkboxValue= $event.target.checked" />
```

 第一行的代码其实只是第二行的语法糖。
 问题是：click方法中使用了变量`this.checkboxValue`,因此如果是先触发了`change`事件，对checkboxValue进行了赋值。之后再触发`click`那么获取的结果就是正确的。
 有了以上想法之后：对`change,click`事件做了实验
实验浏览器版本：

```
IE(11.0.9600.18977)`
`Firefox(52.7.3)`
`Chrome(66.0.3359.139)
```

 Firefox / Chrome: `先执行click事件，后执行change事件`
 IE: `先执行change事件，后执行click事件`

### 3. 解决方法

#### 方法一：直接获取checked的值

```
<template>
  <div class="hello">
    <input type="checkbox" v-model="checkboxValue" @click="onClick($event)"/>
  </div>
</template>
<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      checkboxValue: false
    }
  },
  methods:{
    onClick(event){
      console.log(event.target.checked)
    }
  },
}
```

#### 方法二：使用@change进行监听，等值变化了再使用

```
<template>
  <div class="hello">
    <input type="checkbox" v-model="checkboxValue" @change="onChange"/>
  </div>
</template>
<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      checkboxValue: false
    }
  },
  methods:{
    onChange(){
      console.log(this.checkboxValue)
    }
  },
}
```

------

作者： [Jessy Hong](http://jessyhong.github.io/)

