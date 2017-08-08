## HTTP协议

- 浏览器和服务器之间的通信是基于请求和响应的模式进行的
- 浏览器向服务器发送请求报文，服务器向浏览器返回响应报文
- HTTP协议就是用来规定请求和响应报文的格式的
- 报文的格式：
    
    - 首行
    - 头
    - 空行
    - 体

- 请求报文

    - 请求首行
    - 请求头
    - 空行
    - 请求体
        
            请求体浏览器通过请求提向服务器发送请求参数。
- get 和 post

    1. 除了将表单的method属性设置为post，其余情况都是get请求
    2. get请求通过url地址发送请求参数
    
        - post请求通过请求提发送请求参数
        
    3. get请求的参数在地址栏可见，相对不安全
    
        - post请求参数在请求体中，不可见相对安全
    
    4. url地址栏的长度有限制，不能超过255个字符，所以使用get请求不能发送太多的信息，请求体没有长度限制，可以发送任意大小的数据
    
    5. 一般情况下使用表单向服务器发送数据时，都是使用post请求，而不是get

- 响应报文
    
    - 响应首行
    - 响应头
    - 空行
    - 响应体
    
- 响应状态吗
    
    - 200 响应成功，2开头都是成功相关的
    - 302 重定向，3开头都是重定向相关的
    - 404 页面未找到，4开头的都是客户端错误
    - 500 服务器内部错误，5开头都是服务器错误
   

## HTTP会话控制

- HTTP协议是一个无状态的协议  
    服务器无法直接通过HTTP协议来区分出请求是否发送自同一个请求

- cookie , 在HTTP协议中我们可以通过cookies来识别浏览器用户

- cookies的使用流程
    
    1. 服务器制作并发送cookies给浏览器
    2. 浏览器将cookies保存
    3. 浏览器带着cookies再次访问服务器
    4. 服务器根据cookies来识别浏览器

- cookies实际上就是一个头

    - 服务器将cookies以响应头的形式发送给浏览器
    - 浏览器收到该响应头
  
### http缺点  
1.  无法实时真正意义上的长链接
2.  每次请求响应都会附加很多的信息
3.  无法保持会话状态
4.  半双工通讯方式，效率低下
5.  无法实现跨域访问


## Express

### 路由 Route
- 路由简单来说就是Express中处理用户请求的组件当用户访问服务器时，服务器必须有对应的路由来进行影射
- 路由作用就是将用户的请求和服务器中的程序进行影射路由是将url地址和回调函数做了一个影射

#### 设置路由：

        app.<method>(path,callback)
            - <method> 表示路由的请求方法
                - get 设置get请求的路由
                    - app.get()
                - post 设置post请求路由
                    - app.post()
            - path 
                路由要影射的路径
            - callback
                回调函数，路由被访问时，将会调用该函数来处理用户的请求，
                回调函数中有两个参数：
                request:请求对象，封装了用户请求的信息
                response：响应对象，封装了服务器发送的响应报文

- 也可以将路由统一设置到Router对象上面 

        const router = express.Router();
        router.get("/",...)
        router.post("/abc",...)
        app.use("/hello",router)
        
### 中间件 Middleware
    
- 中间件和路由的功能很像，不同的是中间件的路径可以省略不写，如果不写会匹配到所有的路径

- 用法：
    
        app.use();


```

//以前的写法
const bodyParser = require("body-parser");
app.use(bodyParser());

//新写法
app.use(bodyParser.Urlencoding({extend:false}) );
app.use(bodyParser.JSON)

```
        
#### url地址
        
        http://192.168.21.32:3000/login?username=admin&password=adddd
        协议：//ip地址：端口号/路径 ? 查询字符串

#### 路径

    虚拟路径
          http://192.168.21.32:3000/daisy.jpg  
     真实路径
          D:\WebStorm\node\express_demo01\public\daisy.jpg  
          
- 相对路径

    - 相对于当前资源所在的目录的路径
    - 相对路径可以使用.或者..开头 或者直接写文件的路径
        
            当前文件夹
            ./hello.html 
            
            hello.html
            ../hello.html
- 绝对路径

    - 绝对路径永远相对于服务器的根目录，对于Express来说默认情况的根目录就是public  
    
    - 绝对路径就是使用 / 开头
           
            /hello  -->根目录
    
    - 开发中应该给图片资源使用相对路径而不使用相对路径      
            

#### Response
    
- 属性和方法

    1. send([satatus,]body)  
      - 设置响应状态码，和响应体
     
    2. download(path,filename)  
      - 提供下载文件
    
    3. render()  
      - 渲染EJS
      
## EJS

```
        
//配置
app.set( "views","views" )；

//渲染
app.get("/ejsTest",(req,res)=>{

    //app.locals中的信息每一个用户看到的都一样，全局
    app.locals.username = "猪八戒"；
    
    //res.render("hello.js") 渲染模板，不传变量
    
    //也可以将变量设置到res的locals属性中，比较私密，当前请求
    res.locals.username = "沙和尚"； 当前请求
        
    res.render("hello.ejs", {username:"孙悟空"})；   

} )


<%=username%> 
   
    执行JS代码并将代码转义后输出
    脚本语言在服务器端执行，浏览器看不到

<%-"<div>hello</div>"%> ---> 
    
    执行JS代码 并直接输出

<% console.log("hello")%> ---> 
    
    直接执行JS代码，没有输出    
    在服务器端控制台打印，
        
```    
  
    
    