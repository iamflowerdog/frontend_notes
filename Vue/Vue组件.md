## 1.Vue组件的定义与使用
### 一个.vue文件就是一个vue组件

```
1. 组件是Vue.js最强大的功能之一
2. 扩展HTML元素
3. 封装可重复使用的代码
4. 较高层面上，组件是自定义元素，Vue.js编辑器为他添加特殊功能
```

#### 注册组件

* 创建一个Vue实例

```
new Vue({
  el: '#some-element',
  // 选项
})
```

* 注册一个全局组件 `Vue.component(tagName, options)`

```
Vue.component('my-component', {
  // 选项
})
```

> 对于自定义标签名，Vue.js 不强制要求遵循 W3C 规则 (小写，并且包含一个短杠)，尽管遵循这个规则比较好。




#### 组成部分(3个部分)

```
1.模板页面: 
      <template>
        页面模板
      </template>
2.JS模块对象: 
  <script>
    export default {
      data() {return {}},
      methods: {},
      computed: {},
      components: {}
    }
  </script>
3.样式: 
  <style scoped>  //scoped代表样式只针对当前组件的模板页面
    样式定义
  </style>
```

### 基本使用

* 在父组件中配置子组件标签

```

<template>
  <hello>
</template>
<script>
  import Hello from './components/Hello'
  export default {
    components: {
      Hello
    }
  }
</script>

```

## 关于标签名和属性名书写的问题

```
1.标签名与标签属性名不区分大小写
2.标签名: 如果组件名是XxxYyy, 标签名必须为<xxx-yyy>
3.属性名: 如果标签属性名为xxx-yyy, 组件得到的属性名为: xxxYyy

```

## data必须是函数

* 通过Vue构造器传入的各种选项大部分都可以在vue里面使用，data是例外必须是函数
* 如果执意要做会报错，报错提示你data必须是函数

```
let data = {counter: 0};

Vue.component("my-component", {

    data(){
        return data
    },

    template: '<button v-on:click="counter++">{{counter}}</button>'
});

new Vue({

    el: '.example'

});

//The "data" option should be a function that returns a per-instance value in component definitions.
```

## 构成组件

* 父组件给子组件传递数据，
* 子组件告诉父组件它内部将要发生的事情
* 良好定义的接口中尽可能将父子组件解耦是很重要的
* `Vue`中，父子组件关系是 `props down, events up`

![image](https://cn.vuejs.org/images/props-events.png)


## DOM模板解析说明

* 将 `el` 选项挂载到一个已存在的元素上面，会收到html的限制

```
<table>
  <my-row>...</my-row>
</table>
```

* 解决方案

```
<table>
  <tr is="my-row"></tr>
</table>
```

> 使用字符串模板，这些限制将不适用

* `<script type="text/x-template">`
* JavaScript 内联模版字符串
* `vue`组件

## camelCase vs. kebab-case

* HTML特性是不区分大小写的，所以当使用的不是字符串模板需要转换

```
<div class="test">
    <child my-msg="world"></child>
</div>

Vue.component('child', {
    props: {
        myMsg: String
    },
    template: '<p>hello --- {{myMsg}}</p>'
});

new Vue({
    el: '.test'
});

// myMsg ----> my-msg

```





