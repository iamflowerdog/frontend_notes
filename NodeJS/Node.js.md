# node.js简介
- 进程是任务，线程是干活的人
- Node 实际就是一款对ES标准实现的JavaScript引擎
- Node是一款非阻塞I/o web服务器

        alert()阻塞函数，主线程不用等。
- Node的底层是由C++编写的
- Node可以让JavaScript代码执行运行在系统中，和系统的底层进行交互
- Node的特点：
    1. 非阻塞、异步I/O
    2. 事件、回调函数机制
    3. 单线程
        - 单主线程，(线程池)分线程
    4. 跨平台
        - Node可以在不同操作系统中使用
- NPM Node中的模块管理工具

### exports 和 module.exports 的区别

- nodejs的系统底层自动给nodejs文件增加了2个变量exports和module,
- module又有一个属性exports,这个属性值指向一个空对象{};
- 而同时exports这个变量也指向了这个空对象{}，于是就有了

    
```
graph LR
A[module.exports]-->B["{ }"]
C[exports]-->B
```
- 这两个exports其实没有直接关系，他们初始值都指向同一个空对象{}；
- 如果其中一个不指向这个空对象了，那么他们就没有直接关系了；

    

1. module.exports初始值为一个空对象{}  
2. exports是指向的module.exports的引用
3. require()返回的是module.exports而不是exports

- 我们经常看到这样的写法:

        exports = module.exports = somethings
        
- 上面的代码等价于:

        module.exports = somethings
        exports = moudule.exports

- 通过修改module.exports这个变量的引用对象来暴露出对象

        module.exports = mongoose.model("user" , userSchema);//暴露一种方法
        
        module.exports = {
            jiecheng:jiecheng,
            sum:sum,
            min:min,
            multiple:multiple
        };//暴露多种方法

- 通过exports的引用对象往里面添加属性

        exports.addDoter = addDoter;
        exports.findDoterByName = findDoterByName;
        exports.findDoterById = findDoterById;

原理很简单，module.exports 指向新的对象时，exports还是指向原来空对象的引用，通过exports = module.exports重新指向module.exports即可。

- 引用

```

//将路由对象导出
exports.userRouter = userRouter;

//module.exports = userRouter;

```







    