## Vue简介

#### Vue特点

1. Vue.js（读音 /vjuː/，类似于 view） 是一套构建用户界面的渐进式框架。
2. Vue 的核心库只关注视图层。
3. 声明式渲染。
4. 所有的元素都是响应式的。

#### 双向数据绑定

* 不用直接操作页面，更改数据就可以更新页面
* Vue底层在帮我们做这些事情


#### Vue模板

1. `template` 里面有自定义标签，浏览器不识别
2. 模板获取数据更方便，比原生获取简单

#### Vue对象

* Vue是个函数对象可以直接打印出来

```
function Vue$3(options) {
  if ("development" !== 'production' &&
    !(this instanceof Vue$3)
  ) {
    warn('Vue is a constructor and should be called with the `new` keyword');
  }
  this._init(options);
}
```

* Vue是个构造函数，必须用new关键字创建vue实例

```
var app = new Vue({
        el: "#app",
        data: {
            msg: "Hello Vue!"
        }
    });
    
app.$data // Object {__ob__: Observer}

```
* 要想访问Vue的data属性，必须加上 $ 符号
* 可以通过 app.msg / app.$data.msg 修改数据

```
app.msg = "Hello Dota2";
app.$data.msg = "hello juggernaut";

```

#### 声明式渲染指令

*  `v-bind`属性被称为指令，指令带有 `v-` 以表示他们是特殊的Vue提供的特殊属性
*  作用: 将这个元素节点的title属性和Vue实例的msg属性保持一致
*  `Vue`定义的标签属性 如 `v-cloak` 为 `Vue` 指令

```
<span v-bind:title="msg">
    鼠标悬停几秒钟查看此处动态绑定的提示信息！
</span>


let app = new Vue({
    el: "#app",
    data: {
        msg: "页面加载于：" + new Date()
    }
})

```
* `v-if` 条件判断，可以绑定DOM结构数据

```
<div id="app">
    <p style="color: deeppink" v-if="seen">你看不见我</p>
</div>

let app = new Vue({
        el: "#app",
        data: {
            seen: true
        }
    })
```

* `v-for `可以绑定一个数组的数据，来渲染一个项目列表

```

<div id="app">
    <ol>
        <li v-for="hero in heroes">
            {{hero}}
        </li>
    </ol>
</div>
    
let app = new Vue({
    el: "#app",
    data: {
        heroes: [
            "invoker", "juggernaut", "lina"
        ]
    }
});

app.heroes.push("rubic");
app.heroes.unshift("sven");

```

* `v-on` 绑定一个事件监听器，可以让用户和应用互动

```
<div id="app">
    <h1 style="color: deeppink; text-align: center">{{msg}}</h1>

    <h2>{{msg}}</h2>

    <button v-on:click="Reverse">翻转按钮</button>
</div>


let app = new Vue({
    el: "#app",
    data: {
        msg: "Defence Of The Ancients!"
    },
    methods: {
        Reverse(){
            this.msg = this.msg.split("").reverse().join("");
        }
    }
});
```

* `v-model` 表单和应用状态之间双向数据绑定

```
<div id="app">
    <h1>{{msg}}</h1>
    <input type="text" v-model="msg">
</div>

let app = new Vue({
    el: "#app",
    data: {
        msg: "dota2"
    }
})
```

* `v-bind`缩写  

```
<!-- 完整语法 -->
<a v-bind:href="url"></a>
<!-- 缩写 -->
<a :href="url"></a>
```

* `v-on`缩写

```
<!-- 完整语法 -->
<a v-on:click="doSomething"></a>
<!-- 缩写 -->
<a @click="doSomething"></a>
```

#### 计算属性

* computed 复杂的逻辑建议使用计算属性

```
computed?: { [key: string]: ((this: V) => any) | ComputedOptions<V> };
```

* 实际应用翻转字符串

```
<div id="app">
    <h1 style="color: deeppink; text-align: center">{{msg}}</h1>

    <h2>{{ReverseMsg}}</h2>

</div>

let app = new Vue({
    el: "#app",
    data: {
        msg: "Defence Of The Ancients!"
    },
    computed: {
        ReverseMsg(){
            return this.msg.split('').reverse().join('');
        }
    }
});
```

* 这里我们声明了一个计算属性 `ReverseMsg`, 函数将作用属性`app.ReverseMsg`的 getter.
* 计算属性是基于它们的依赖进行缓存的
* 计算属性只有在它的相关依赖发生改变时才会重新求值