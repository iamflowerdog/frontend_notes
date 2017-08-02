## Database

- 数据库就是用来存储数据的仓库
- 通过数据库可以对程序运行时产生的数据进行 持久化 操作；
- 通过数据库可以对数据进行存储，查询，修改，删除
- 关系型数据库(存的表)MySQL Oracle
- MongoDB 属于NoSQL数据库(不适用SQL查询)
- MongoDB基本概念

    - Database 数据库
    - Collections 集合
    - Document 文档 BSON 二进制JOSN格式

## db.tables.save()
- 和db.tables.insert()类似，但是insert()可以无限插入下去
- 插入文档你也可以使用 db.col.save(document) 命令。如果不指定 _id 字段 save() 方法类似于 insert() 方法。如果指定 _id 字段，则会更新该 _id 的数据。

## db.tables.find().pretty()
- 方法以格式化的方式来显示所有文档。

## db.tables.findOne()
- 只返回第一个文档，可以传两个对象，但是记得给对象中的属性名加上引号；不然查不出来

## db.tables.find({$or:[{},{}]) 
    db.books.find({$or:[
                    {name:"rubic"},
                    {name:"haha"}
                    ]})
- 只要满足其中任何一个属性值，就是的

## and和or联合使用
    db.books.find({
                    "age":{$gt:"10"},
                    $or:[{name:"rubic"},
                    {name:"haha"}]
          })

## update()
- 默认情况下只会修改一个，可以将{multi:true}作为第三个参数传递，此时update将会更新多个文档

## db.doters.getIndexes()
- 获取集合的索引版本

## db.doters.deleteMany({})
- 删除集合中的所有用户

## db.doters.drop()
- 删除整个集合

## 修改器
- $set 


## collection


```
graph LR
A[Databases]-->C{Collectios}
C-->|约束对象| D[document]
C-->|Schema| E[集合名]
C-->|Model对象| F{doters}
F-->|实例|G[文档对象]
F-->|实例|H["hero:invoker"]

```



