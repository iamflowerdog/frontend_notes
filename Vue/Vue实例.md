## Eslint

* 状态码

    1. 0 默认值，不检查,关闭规则
    2. 1 警告 打开规则 不影响exit code
    3. 2 报错 打开规则 并且作为一个错误

* 支持的框架

    1. ES6
    2. Angular
    3. JSX
    4. style检查
    5. 自定义错误和提示
    
## mouseover mouseout / mouseenter mouseleave 

* 嵌套div的时候，从外层div进入内层div会触发mouseout
* mouseenter 则不会触发

## 实例

#### 构造器

* 每个Vue.js应用都是通过构造函数Vue创建一个Vue的根实例启动的

```
var vm = new Vue({
  // 选项
})
```

* Vue设计受 `MVVM模式` 启发，但没有完全遵循它的模式
* 实例化时，需要传入一个 `选项对象` 
    
#### 选项对象

* 选项对象可以配置内容

    1. 数据 `data`
    2. 模板 `template`
    3. 挂载元素 `el`
    4. 方法 `methods`
    5. 生命周期钩子 `create...`

#### 可以扩展 `Vue` 构造器，创建复用的 `组件构造器`

```
var MyComponent = Vue.extend({
  // 扩展选项
})
// 所有的 `MyComponent` 实例都将以预定义的扩展选项被创建
var myComponentInstance = new MyComponent()
```

#### 每个Vue实例都会代理其`data`对象里所有的属性:

```
var data = { a: 1 }
var vm = new Vue({
  data: data
})
vm.a === data.a // -> true
// 设置属性也会影响到原始数据
vm.a = 2
data.a // -> 2
// ... 反之亦然
data.a = 3
vm.a // -> 3

```
* 被代理的属性是 `响应的` ， 值的改变会触发重新渲染视图
* 注意： 在实例创建之后添加新的属性，不会触发视图更新


#### 实例属性和方法 `vm.$el/vm.$data/vm.$watch`

* 除了data属性，Vue实例暴露了一些有用的实例属性和方法，这些方法前缀都有 `$` , 以便与代理的data属性区分。例如:

```
var data = { a: 1 }
var vm = new Vue({
  el: '#example',
  data: data
})
vm.$data === data // -> true
vm.$el === document.getElementById('example') // -> true
// $watch 是一个实例方法
vm.$watch('a', function (newVal, oldVal) {
  // 这个回调将在 `vm.a`  改变后调用
})
```

### 实例生命周期

* 实例初始化

    1. 实例需要配置数据观测(data observe)
    2. 编译模板
    3. 挂载实例到DOM
    4. 数据变化时更新DOM

* 实例初始化过程中，实例也会调用一些 `生命周期钩子`
* 这样我们就可以执行自定义逻辑，例如 `created` 钩子在实例被创建之后被调用：

```
var vm = new Vue({
  data: {
    a: 1
  },
  created: function () {
    // `this` 指向 vm 实例
    console.log('a is: ' + this.a)
  }
})
// -> "a is: 1"
```

* 生命周期钩子列表

    1. `created`
    2. `mounted`
    3. `updated`
    4. `destroyed`
    
* 钩子的 `this` 指向调用它的Vue实例
    

* Vue.js没有 `控制器` 的概念，组件的自定义逻辑可以分布在这些钩子中

### 生命周期图示


![image](https://cn.vuejs.org/images/lifecycle.png)
