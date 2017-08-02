# 简介
- 异步的JavaScript和XML
- Ajax可以通过js异步的向服务器发送请求，并通过DOM将相应的信息在页面刷新出来，不需要刷新整个页面，xml是服务器返回的数据格式

        <student>
            <name>invoker</name>
            <age>76</age>
        </student>
        
        //这种方法已经被JSON淘汰

#### Ajax的优点

1. 不需要刷新整个页面，提高用户体验
2. 大量使用Ajax的页面不利于SEO
3. 是服务器和页面完全分离

#### Ajax的缺点

1. 通过Ajax发送的请求无法用回退按钮返回
2. 大量使用Ajax的页面不利于SEO
3. 同源策略

        $.get(
               "http://localhost:3000/JsonP",
               {username:"$.get方法", password:"456789"},
               (data) => {
                   alert(data);
               },
               "JSON"
         ) 
        
        通过浏览器http://127.0.0.1:3000/JsonP ，发送请求不成功由于非同源

### 使用步骤

1. 创建xhr对象
    
        var xhr = newXMLHttpRequest();

2. 设置请求信息

        xhr.open("method","url");

3. 发送请求

        xhr.send(请求体)；
        
4. 接收响应

        xhr.onload = function(){
    		if(xhr.readyState == 4 && xhr.status == 200){
    			//xhr.resopnseText
    		}
    	}



## setRequestHeader

        xhr.setRequestHeader("Content-Type","application/x-www-form-urlencoded");
        使用ajax提交post请求时，它的请求头必须有如下的一个设置
        如果不设置请求参数将无法正常解析

## 