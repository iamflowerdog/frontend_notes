## 理解rest
  * api接口的分类
    * restful: rest风格
    * restless: 非rest风格
  * rest接口
    * http://localhost/users
    * http://localhost/users/2
    * 不用带行为参数, 参数是路径的一个节点
    * 请求的行为由请求方式来决定
      * get: 查询(读, 获取数据)  R read
      * post: 添加(保存), C create
      * delete: 删除, D delete
      * put: 更新, U update
  * 非rest接口
    * http://newsapi.gugujiankong.com/Handler.ashx?action=getusercomments&userid=514
    * 可以带上行为参数, 通过key=value的形式携带
    * 一般只有2种请求式:
      * get
      * post
## 模拟实现rest接口
  * 使用json-server库
  * 使用:
    * 下载 json-server
    * 创建一个数据库文件: src/mock/db.json
    * 启动服务器: json-server --watch src/mock/db.json
  * 编码测试访问rest接口
    * axios
    * axios.get(): get请求, 查询
    * axios.post(): post请求, 保存
    * axios.put(): put请求, 更新
    * axios.delete(): delete请求, 删除
