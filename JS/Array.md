# 数组

#### 1. 数组也是一个对象，数组是专门用来存储数据的对象
#### 2. 数组使用索引(index)来操作数据而不使用属性名
#### 3. 由于数组存储方式的不同，数组的存储性能高，开发用数据组存储数据


### 创建一个数组

        var arr = new Array();
        typeof arr // object;

## 非连续数组

        arr[0] = 1 ;
        arr[2] = 3 ;
        arr[9] = 10;
        
        arr.length // 10 ,自动补全，不建议开发中用
        arr.length = 11; // 设置数组长度，后面的用undefined代替
                            (11) [10, 8, 6, 4, 2, undefined × 5]

## Array.concat()  拼接数组

    var array = [1, 2, 3, 4];
    arr.concat([5, 6, 7]) // [1, 2, 3, 4, 5, 6, 7];

## Array.pop() 删除并返回数组的最后一个元素 

- pop英文原译：子弹碰碰声，打出去第一颗子弹

    var arr = [1, 2, 3, 4];

    console.log(arr.pop());//4

    console.log(arr);//(3) [1, 2, 3]
    
## Array.shift() 删除并返回数组第一个元素

    var arr = [1, 2, 3, 4];

    console.log(arr.shift());//1

    console.log(arr);// (3) [2, 3, 4]

## Array.unshift() 在数组头部插入一个元素 并返回数组的长度

    var arr = [1, 2, 3, 4];

    console.log(arr.unshift(0));//5

    console.log(arr.shift());//0

    console.log(arr);// (5) [0, 1, 2, 3, 4]
    
## Array.push() 向数组末尾添加一个元素 并返回数组长度

    var array = [1, 2, 3, 4, 5, 8, 3, 5];

    console.log(array.push(0));//返回数组长度9，向数组末尾添加一个元素

    console.log(array);//(9) [1, 2, 3, 4, 5, 8, 3, 5, 0]
    

## Array.slice(start, end) 截取数组的一部分，不修改原数组

#### start 开始截取，不包含end，如果是负数从后面开始计数

    var arr = [1, 2, 3, 4, 5];

    console.log(arr.slice(1, -1));//(3) [2, 3, 4]

    console.log(arr);// (5)  [1, 2, 3, 4, 5]
    
## Array.join() 将数组转换为字符串并返回

    var arr = [1, 2, 3, 4, 5];

    console.log(arr.join());//1,2,3,4,5
    
    console.log(arr.join("@"));//1@2@3@4@5 可以传参数用来连接字符串

    console.log(arr);// (5)  [1, 2, 3, 4, 5]

## Array.reverse() 颠倒数组的排序，改变原数组

    var arr = [1, 2, 3, 4, 5];

    console.log(arr.reverse());//(5) [5, 4, 3, 2, 1]

    console.log(arr);// (5) [5, 4, 3, 2, 1]
    
## Array.splice(start, count, insert) 从start开始删除count个数组元素，并向里面insert元素

    var arr = [1, 2, 3, 4, 5];

    console.log(arr.splice(2, 0, "invoker", "axe"));//[]

    console.log(arr);// (7) [1, 2, "invoker", "axe", 3, 4, 5]
    
## Array.join(),把数组转换为字符串，默认用 ',' 分隔

    var str = "hello";

    var strArray = str.split(""); //(5) ["h", "e", "l", "l", "o"]

    var strReverse = strArray.reverse(); //(5) ["o", "l", "l", "e", "h"]

    console.log(strReverse.join("")); //olleh
    
## 数组去重

```
/*
   思路：
   1.创建一个新的数组存放结果
   2.创建一个空对象
   3.for循环时，每次取出一个元素与对象进行对比，如果这个元素不重复，则把它存放到结果数组中，
      同时把这个元素的内容作为对象的一个属性，并赋值为1，存入到第2步建立的对象中。

    说明：至于如何对比，就是每次从原数组中取出一个元素，
     然后到对象中去访问这个属性，如果能访问到值，则说明重复。
   */
   
    //原生js方法
    let let arr3 = [7, 9, 7];
    
    function unique(arr) {
        let arr1 = [];
        let obj = {};
        for (let i=0; i<arr.length; i++){
            //console.log(arr[i]);
            //console.log(obj[arr[i]]);
            if (!obj[arr[i]]){

                arr1.push(arr[i]);
                //obj[arr[i]] = i;当写i时，obj：{7: 0} 也就是obj[arr[i]]: 0;
                obj[arr[i]] = 1; // 没有属性时添加属性 obj：{7: 1}

            }
        }
        console.log(obj);
        return arr1;
    }
    
    

```

# ES6 Array 新方法

## ...array

    let arr1 = [1,3,5];
    let arr2 = [2,...arr1,6];

    console.log(arr2); //(5) [2, 1, 3, 5, 6]

    arr2.push(...arr1);

    console.log(arr2); //(8) [2, 1, 3, 5, 6, 1, 3, 5]
    

## 数组去重

    let arr = [1, 4, 2, 4, 3, 6, 3, 5, 5];

    //通过ES6 Set 容器方法去重
    let setArr = new Set(arr);

    setArr = Array.from(setArr)

    console.log(setArr);//(6) [1, 4, 2, 3, 6, 5]
