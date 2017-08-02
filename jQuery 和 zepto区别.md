## prop()和attr()区别

1. prop多用在标签的固有属性，布尔值属性！(类似于element.currenStyle.attribut)
2. attr多用自定义属性上面，查询不到会返回undefined(类似于element.style.attribute)

```
//HTML代码
<select style="font-size:25px;">
	<option value="">科比</option>
	<option value="">韦德</option>
	<option value="" selected="selected">邓肯</option>
	<option value="">吉诺比利</option>
	<option value="" selected="selected">艾弗森</option>
</select>

//JS代码
$(document).ready(function () {
	$("option").each(function (index, items) {
        console.log(index, $(items).attr("selected"));
        //0,1,3返回undefined 和 2,4返回selected
        console.log(index, $(items).prop("selected"));
        //0,1,2,3返回false，只有4返回ture，因为3的selected在页面执行时被覆盖了，相当于没生效
    })
})

```

## $.each()

- jQuery 不可以遍历字符串
- zepto 可以遍历String
- zepto 可以变量JSON

```
var obj = {
            name: "invoker",
            age: 18
        };

obj = JSON.stringify(obj);

$.each(obj, function (key, value) {
    console.log(key, value);
});

var str = "hello";

$.each(str, function (index, value) {
    console.log(index, value);
});

//输出结果：0 "h", 1 "e"....

```

## $(element).offset();

- zepto返回一个对象，不仅可以返回left和top，还可以返回height和width
- jQuery只有left 和 top

        Object
            height: 224
            left: 50
            top: 50
            width: 224
            __proto__: Object
    
## $(element).width();

- zepto中的width(),height()是根据盒模型来取值的，包含border，留白的值

        $("#box").width()；//226 没有单位，width + padding + border
        
- zepto没有innerHeiht(),innerWidht()

- zepto通过.css获取的width，height是内容区的宽高，包含单位

        $("#box").css("width") // 200px width 内容区高度
        $("#box").css("border-width") // 3px 


## $(element).delegate(".box", "click", callback);

- 通过冒泡原理来完成事件委托

        $(parent).delegate(child, event, callback)
        
- 在zepto里面统一用on来替代delegate

         $(parent).on(event, child, callback)；

## serialize() 

- 在Ajax post请求中将表单元素提交的值编译成URL-encoded 返回名值对，字符串形式

        
```
<form method="post">
    <input type="password" name="pw" value="123"/>
    <input type="text" name="val" value="kobe"/>
    <input type="checkbox" checked="checked"  name="rember"/>
    <input type="submit" value="按钮" name="anniu"/>
</form>

$("form").serialize();//pw=123&val=kobe&rember=on

```
## serializeArray()

- 将post请求中表单的元素的值编译成拥有name和value对象的数组。
- 不能提交button元素的value 和name值，未选中的radio buttons/checkboxs 将会被跳过。

```
$("form").serializeArray(); 

//输出结果
(3) [Object, Object, Object]
        0:Object
            name: "pw"
            value: "123"
            __proto__: Object
        1:Object
        2:Object
        length:3
        __proto__:Array(0)
```
## submit()
- 为 "submit"事件绑定一个处理函数，或者触发元素上的 "submit"事件
- 函数不传递回调函数的时候，当前的表单 "submit"会一直触发

        $("form").submit();//不建议，会一直提交数据
        
        $("form").submit(function (event){
            
            event.preventDefault(); //阻止默认行为
            var data = $(this).serializeArray();
            console.log(data);
        });

> 注意：setTimeout(funtion(){},1000),是window对象
    