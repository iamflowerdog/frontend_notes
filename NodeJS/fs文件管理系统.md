# 文件系统(file system) 
- node 通过文件系统来对计算机各种文件进行读写操作。
- fs中的方法都是分成两种：异步方法(不带sync) 同步sync
- 异步方法不会阻塞程序执行的，同步方法会
- 适用fs，需要先对fs进行引入
    
        let fs = require("js");

## fs.openSync(path, flags[, mode])
- path:文件路径
- flags：读写方式，打开文件模式  
    - "r" 读取模式打开，如果不存在则发生异常
    - "w" 以写入模式打开，如果不存在则创建或被截断
    
- mode：文件权限设置(在windows中不常用)可省略  


## fs.open(path, flag[,mode],callback)  


- callback 文件打开之后的回掉函数
    
    - err ： 报错信息
    - fd： 文件描述符(一般是从3开始，0，1，2被占用)




