## Map数据结构干什么的？

- ES6提供新的数据结构，类似于对象，也是键值对的结合，但是key的范围不限于字符串，对象都可以当作key。

```
let map0 = new Map()
  .set(1, 'a')
  .set(2, 'b')
  .set(3, 'c');

let map1 = new Map(
  [...map0].filter(([k, v]) => k < 3)
);
// 产生Map结构 {1 => 'a', 2 => 'b'}
```

#### 补充: Set 数据结构

- ES6 提供了新的数据结构 Set。
- 类似于数组，但元素的值是唯一的，没有重复的值

```
// 例一
const set = new Set([1, 2, 3, 4, 4]);
[...set]
// [1, 2, 3, 4]
```

## class 类中super对象到底是什么？

//...

## github 怎么取消对某个项目的关注?

//... repository--->setting--->Danger Zone-->delete

## React组件在渲染时候，里面是否可以添加html标签？

- 可以

## name变量在js中为什么可以提前解析？

```
console.log(name, a, names);

var name = "我是全局中的name"; // ----> name 变量 在浏览器解析中会提前预解析
var a = "3";
var names = "我是names"

```

- 答: 因为window里面有name属性

## 用vue-cli脚手架  下载 webpack的模板  #app是怎么渲染到的？

* webpack 会打包编译到 index 一个script标签下面



## 外原型里面添加方法，怎么调用类自己的属性？

```
function Parent(name, age) {
    var hero = "invoker";
    this.name = name;
    this.age = age;
    this.sayName = function () {
        console.log(name);
    }
}

Parent.prototype.sayAge = function () {
    console.log("sayAge()", hero);
};
```

* 答： 在执行函数定义的时候函数的显示原型对象自动创建

    `Parent.prototype={}`

## 怎样查看函数对象本身里面的方法 call() apply() ?

* 通过for in 遍历 ，或者 查看 Object的方法


