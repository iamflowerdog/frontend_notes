## <b></b>

#### 定义和用法
<b>标签规定粗体文本  
#### 提示和注释
**注释**： 根据HTML5规范，在没有其他更合适的标签时候，才应该把<b>标签作为最后的选项。

## <form>

```
<form action="/user/upload" method="post" >

    //action:指向路由地址，method：表单提交方式，有get和post
    
     用户名 <input type="text" name="username"> <br> <br>
     //设置multiple="multiple" 可以一次上传多个图片
     //通过multer解析时候，必须用 upload.array("photo")接收
     照片  <input type="file" name="photo" multiple="multiple"> <br> <br>
    <input type="submit" value="提交"> <br> <br>
    
    //提交图片信息，需将input的type属性设置为file
    //并且form表单接收编码(enctype )的方式设置为 multipart/form-data
    //这个参数表示表单将会以多部件表单形式上传
    //默认enctype="application/x-www-form-urlencoded" 
    //通过url编码解析格式为：username=%E5%AD%99%E6%82%9F%E7%A9%BA
    //Content-Type:multipart/form-data; boundary=----WebKitFormBoundaryVSKNY4CZBdbh7oE5
    //通过多部件方式解析，Request Headers 会有这样的提示
    //boundary=----代表分界线，每个表单部件之间用分界线划分

</form>

```

