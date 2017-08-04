##select标签
#####用法：创建带有 4 个选项的选择列表：
```html
<select  name = "h1"  multiple="multiple">
	<option value ="value"> Volvo </option>
	<option value ="value"> Volvo </option>
	<option value ="value"> Volvo </option>
	<option value ="value" selected="selected"> Volvo </option>
</select>

// 可以设置selected默认被选中
```
<!--<font face="微软雅黑" color=blue size=5>我是黑体</font>-->


----------
##### 定义和用法
select 元素可创建单选或多选菜单。
`<select>`元素中的`<option>`标签用于定义列表中的可用选项。

----------
<font color=orange>**提示:**</font>select元素是一种表单控件，可用于在表单中接受用户输入。

----------

**属性:**
multiple 属性规定可同时选择多个选项。  
在不同操作系统中，选择多个选项的差异：
- 对于 windows：按住 Ctrl 按钮来选择多个选项 
- 对于 Mac：按住 command 按钮来选择多个选项 

----------
**扩展**
HTML中属性ID和属性NAME有何区别？
- 相同点：两者都是可以用来标识一个标记，JS中分别有两个方法来获取Dom节点。  
		- getElementById  
		- getElementByName  
		
- 不同点：  
    1，在做网页Post提交时，是以Form为单位(表单域)提交的，一个Form里面有若干个表单对象，同一个页面里面可以有多个Form，在表单提交到服务器端后，可以通过Name属性获取到表单域的值，却无法通过ID直接获取该表单对象的值。 

    2，ID属性是全局的，整个html页面里只能有一个；同一个Form里不能有多个name属性相同的HTML标记，但是一个网页如果可以有多个Form，则不同的Form里面可以同个Name属性的标记。  

    3,在建立CSS样式的时候，可以建立ID样式表(以#为前缀),而无法用Name样式表  









