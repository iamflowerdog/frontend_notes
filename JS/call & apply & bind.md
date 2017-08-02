#### this
   * 根据函数的调用方式不同，this的指向不同
#### call apply
   * 两个都是函数对象的方法，
   * 通过函数对象调用时，call() apply() 函数会立即被执行
   * call()和apply()中可以指定一个参数，这个参数将会
#### call

    ```
     Function.prototype.call = function(thisArg,args) {};
     Function = {};
    ```
#### apply
```
    Function.prototype.apply = function(thisArg,argArray) {};
     @param {Object} [thisArg]
     @param {...*} [args]
     @return {*}
```
#### bind
```
    Function.prototype.bind = function(thisArg,arg) {};
         @param {*} value
         @param {Function|[String|Number]} [replacer]
         @param {Number|String} [space]
         @static
```
* 给foo函数对象绑定this foo.bind(obj)
    ```
    console.log(foo.bind(obj)) //

    print:
         function foo() {
         console.log(this);
         }

    ```
 * 然后再调用通过bind绑定的函数对象
    ` foo.bind(obj)()`



