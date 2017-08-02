## super() 用作函数

- super这个关键字，既可以当作函数使用，也可以当作对象使用，两种用法完全不同

```
   class A {
       constructor(){
           console.log("父类调用了");
       }

   }

   class B extends A {
       constructor(){
           super(); // ------> A.prototype.constructor.call(this)
           console.log("子类调用了");
       }
   }

   let b = new B(); //父类调用了 , 子类调用了
```

- 用作函数super(),只能在子类的构造函数中，其他地方会报错

```
class A {}

class B extends A {
    m(){
        super(); //superclass constructor invocation should in constructor body
                //Uncaught SyntaxError: 'super' keyword unexpected here
    }
}
```

## super 用作对象

- 在子类构造函数中使用 ，super指向父类的原型对象
- 可以直接使用父类原型里面的方法

```
class A {
    constructor(){

    }
    p(){
        return 2;
    }
}

class B extends A {
    constructor(){
        super();
        console.log(super.p());// 2 这里super ----> A.prototype ,可以直接调用父类A的普通方法
    }
}

let b = new B();
```
- super无法使用父类构造函数里面的方法
- 也就是无法使用父类实例上的方法和属性无法获取

```
class A {
    constructor(){
        this.p = 2;
    }
    f(){
        return "f()";
    }
    n(){
        return "n()";
    }
}

A.prototype.x = 8;

class B extends A {
    constructor(){
        super();
        console.log(super.f()); // f()
        console.log(super.n()); // n()
        console.log(super.p); //undefined
        console.log(super.x); // 8 
    }
}

let b = new B();

console.log(b.p); // 2

```

- ES6规定，通过super调用父类的方法时，super会绑定子类的this


```
class A {
    constructor(){
        this.x = 1;
    }
    print(){
        console.log(this.x);
    }
}

class B extends A {
    constructor(){
        super(); //super.print()虽然会调用的时 A.prototype.print()
        this.x = 2; // 但是A.prototype.print() 会绑定子类B的this，导致输出2
    }
    m(){
        super.print();
    }
}

let b = new B();

b.print(); //2 ---> 实际上执行的时super.print.call(this)
b.m(); //2

```

- super无法获取父类实例的的属性和方法

```
//ES6规定，通过super调用父类的方法时，super会绑定子类的this

    class A {
        constructor(){
            this.x = 1;
        }
    }

    class B extends A {
        constructor(){
            super();
            this.x = 2;
            super.x = 3; //等同于 this.x = 3;
            console.log(super.x); //undefined -->super虽然会绑定this，但是super指向还是A.prototype
            console.log(this.x); //this.x
        }
    }

    let b = new B();
    //console.log(b.x); // 3


```

- super在静态方法中指向父类，在普通方法中指向父类的原型对象

```

    class P {
        static foo(msg){
            console.log("static", msg);
        }

        foo(msg){
            console.log("instance", msg);
        }
    }

    class C extends P {
        static foo(msg){
            super.foo(msg);
        }

        foo(msg){
            super.foo(msg);
        }
    }

    C.foo(1); //static 1  子类继承父类的静态方法

    let child = new C();

    child.foo(2); //instance 2


```

- 注意，使用super的时候，必须显式指定是作为函数、还是作为对象使用，否则会报错。

```
    class A {

    }

    class B extends A {
        constructor() {
            super();
            console.log(super.valueOf() instanceof A);
            console.log(super); //SyntaxError: 'super' keyword unexpected here 无法确定super是当作函数，还是对象
        }
    }

    let b = new B();

```

- 可以在任意一个对象使用super关键字

```
//由于对象总是继承其他对象的，所以可以在任意一个对象中，使用super关键字。

    let obj = {
        toString(){
            return "MyObject: " + super.toString();
        }
    };

    console.log(obj.toString()); //MyObject: [object Object]

```




