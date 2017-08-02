## ES6 中的新知识

### 模板字符串

- `` String和变量可以直拼串  用法如下：
            
        `String和${变量}`
```
console.log(`${username} 注册成功`)

可以给变量直接加引号
res.send(`testJsonP('${username}')`);
```

## 变量声明

### let

1. 作用：用于声明一个变量，不能重复声明，不存在提升
2. 应用：块级作用域内声明的变量，外部不可用4


## 结构赋值

    let {a, b} = this.props 
    import {a} from "xxx"

## 对象简洁表达式

    {a, b} 作用域肯定存在变量 a , b

## 扩展运算符

    ...array   拆分对象或者数组


## 指定默认参数

- 传统方法

```
//ES5中通过变通的方法为参数指定默认值

    function point(x, y) {

        if (typeof y === "undefined"){
            y = "world";
        }

        console.log(x, y);
    }

    point("hello");//hello world
    point("hello", "invoker");//hello invoker
    point("hello", "");//hello
    
```

- ES6新语法
```
    //ES6允许为函数的参数设置默认值，即直接写在参数定义的后面

    function arrow(x, y = "world") {
        console.log(x, y);
    }
    arrow("hello");//hello world
    arrow("hello", "China");//hello China
    arrow("hello", "");//hello
    
    function Origin(x=0, y=0) {
        this.x = x;
        this.y = y;
    }

    let o = new Origin();
    o //Origin {x: 0, y: 0}

```

- 参数默认值是惰性求值的

```
    let p = 100;

    function sum(x = p++) {
        return x;
    }

    console.log(sum());//100
    console.log(sum());//101
```

## Class类

- 定义类
- 用 typeof 运算符检查类 返回 函数, 但是不能直接调用
        
        class Foo{
            
        }
        console.log(Foo, typeof Foo); // "function"

```
class Point {
        constructor(x=0, y=0){
            this.x = x;
            this.y = y;
        }
        toString(){
            return '('+ this.x + "," + this.y +')'
        }
    }

    let p = new Point();

    console.log(p); //Point {x: 0, y: 0}
    console.log(p.toString()); //(0,0)
```

- 类的数据类型就是函数，类本身就指向构造函数

```
console.log(typeof Point); //function
console.log(p instanceof Point); //true
console.log(Point.prototype.constructor === Point); //true
console.log(p.__proto__.constructor === Point); //true
```

- 事实上类的所有方法定义在prototype属性上面
- 在类的实例上面调用方法，其实就是调用==class类==原型上的方法

```
//构造函数的prototype属性，在ES6中的类上面继续存在，
 class Name {
    constructor(name, age){
        this.name = name;
        this.age = age;
    }

    sayName(){
        console.log(this.name, this.age);
    }
}

let invoker = new Name("invoker", 19);

console.log(invoker); //Name {name: "invoker", age: 19}

console.log(invoker.__proto__);// Object {constructor: function, sayName: function}

console.log(invoker.__proto__ === Name.prototype); //true

//因为实例的隐式原型指向类的显示原型，所以实例都可以用里面的方法
invoker.sayName();//invoker 19

```

## Class类中this的指向

- 类的方法内部如果含有this，它默认指向类的实例，但是单独使用该方法，很可能会报错

```
   class Logger {

        printName(name = "there"){
            this.print(`Hello ${name}`);
        }

        print(text){
            console.log(text);
        }
    }

    const logger = new Logger();

    logger.printName();//通过实例打印----->Hello there

    const { printName } = logger;

    console.log(printName);//function printName(name = "there"){
                           //     this.print(`Hello ${name}`);
                           //     }

    printName();//Cannot read property 'printName' of undefined


```

* 上面代码中printName 方法的中this 默认指向Logger的实例，但是如果将这个方法提取出来用，this会指向该方法运行环境，因为找不到this而报错，可以在构造方法中绑定this

```
class Logger {
  constructor() {
    this.printName = this.printName.bind(this);
  }

  // ...
}
```

* 还有另外一种方法是使用箭头函数

```
class Logger {
  constructor() {
    this.printName = (name = 'there') => {
      this.print(`Hello ${name}`);
    };
  }

  // ...
}
```

## Class 的静态方法

#### Class的静态方法不会被实例继承

```
//Class的静态方法不会被实例继承
    class Foo {
        static print(){
            return "hello";
        }
    }

    Foo.print(); // 类本身可以调用这个方法

    let foo = new Foo(); // 实例不能继承父类的静态方法

    foo.print();//Uncaught TypeError: foo.print is not a function
    
```
- 上面代码中，Foo 类的 print方法前 有static关键字 ，表示该方法是一个静态方法，可以直接在Foo类上调用，但是类的实例不可以调用


#### 子类可以继承父类的静态方法

```
//Class的静态方法不会被实例继承
    class Foo {
        static print(){
            console.log("hello");
        }

        nice(){
            console.log("world");
        }
    }

    Foo.print(); // 类本身可以调用这个方法

    //子类可以继承父类的静态方法

    class son extends Foo {

    }

    son.print();//hello

    //但子类不可以继承父类的公有方法

    son.nice();//Uncaught TypeError: son.nice is not a function


```

#### 静态方法也是可以从super对象调用的

```
class Foo {
        static print(){
            return "hello";
        }
    }

    class Son extends Foo {
        static print(){
            return super.print() + ", too";
        }

    }
    console.log(Son.print()); //hello, too

```

## Class 的继承

#### Class可以通过extends 关键字实现继承，

```
    class Foo {
        constructor(name="invoker", age=19){
            this.name = name;
            this.age = age;
        }

    }

    class Son extends Foo {
        constructor(){
            console.log(this); //ReferenceError Must call super constructor in derived class before accessing 'this' or returning from derived constructor
            super(); // Son {name: "invoker", age: 19}
        }
    }

    let instance = new Son();

    console.log(instance);
    
```
#### 子类必须在构造函数里面调用super()方法，否则新建实例会报错，原因如下：

1. 子类没有自己的this对象，而是继承父类的this对象
2. 子类可以对父类的this对象进行加工
3. ES6是先创建父类实例对象的this，然后再用子类构造器修改this
4. ES5是先创建子类的实例对象的this，和ES6相反
5. 子类实例的构建，是基于对父类实例加工，只有super()方法才能返回父类实例

```
class Foo {
        constructor(name="invoker", age=19){
            this.name = name;
            this.age = age;
        }

    }

    class Son extends Foo {
        /*
            如果只简单调用super(),不传父类构造函数的参数，
            通过子类创建的实例，是直接通过父类的构造器创建的
             constructor(){
                super();
             }
             new Son("axe", 90, "male")  ----> Son {name: "invoker", age: 19}

         */

        constructor(name, age, gender){
            super(name, age);
            this.gender = gender;
        }


    }

    let instance = new Son("axe", 90, "male");//Son {name: "axe", age: 90, gender: "male"}

    console.log(instance);

```

#### 子类构造器内部 super()

```
    class Foo {
        constructor(){
            console.log(new.target.name);//new.target指向当前正在执行的函数
        }

    }

    class Son extends Foo {
        constructor(){
            super();
        }
    }

    new Foo(); //Foo
    new Son(); //Son

    //注意： super虽然代表父类Foo的构造函数，但是返回的是子类Son的实例
    //即，super内部的this指向Son，因此super()在这里相当于Foo.prototype.constructor.call(this)

```

#### 子类的实例，也属于父类的实例

```
    class Bar {
        constructor(x=1, y=0){
            this.x = x;
            this.y = y;
        }
    }

    class Son extends Bar {
        constructor(x, y, z=0){
            super(x, y);
            this.z = z;
        }
    }

    let a = new Bar(); //Bar {x: 1, y: 0}
    let b = new Son(); //Son {x: 1, y: 0, z: 0}

    //Son是 Bar 的子类，通过Son创建的实例，也属于父类Bar的实例，和ES5一样
    console.log(a instanceof Bar); //true
    console.log(b instanceof Bar); //true
    console.log(a instanceof Son); //false
    console.log(b instanceof Son); //true
```


