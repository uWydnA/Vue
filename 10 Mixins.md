# Mixins

- **类型**：`Array`

- **详细**：

  `mixins` 选项接收一个混入对象的数组。这些混入对象可以像正常的实例对象一样包含实例选项，这些选项将会被合并到最终的选项中，使用的是和 `Vue.extend()` 一样的选项合并逻辑。也就是说，如果你的混入包含一个 created 钩子，而创建组件本身也有一个，那么两个函数都会被调用。

  Mixin 钩子按照传入顺序依次调用，并在调用组件自身的钩子之前被调用。

- **示例**：

  ```html
  <body>
      <div id="box">
          <button @click='getName'>click</button>
      </div>
  </body>
  ```

  ```js
  // 定义一个混入对象
  let myMixin = {
      methods:{
          getName(){
              console.log(1)
          }
      }
  }
  new Vue({
      el:'#box',
      mixins:[myMixin]
  })
  ```

  

- **参考**：[混入](https://cn.vuejs.org/v2/guide/mixins.html)