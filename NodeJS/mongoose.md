# mongoose简介
- Mongoose就是一个让我们可以通过Node来操作MongoDB的模块  

- Mongoose是一个对象文档模型（ODM）库，它对Node原生的MongoDB模块进行了进一步的优化封装，并提供了更多的功能

- mongoose中为我们提供了几个新的对象
    
    1. **Schema**：Schema对象定义约束了数据库中的文档结构
    2. **Model**：Model对象作为集合中的所有文档的表示，相当于MongoDB数据库中的集合collection
    3. **Document**：Document表示集合中的具体文档，相当于集合中的一个具体的文档

```
graph LR
A[Databases]-->B(Model)
B--> C{Collectios}
C-->|约束对象| D[user]
C-->|Schema| E[students]
C-->|Model对象| F{doters}
F-->|实例|G[文档对象]
F-->|实例|H["hero:invoker"]

```








# Schema对象
    
    //创建约束对象
    let doterSchema = new Schema({
        name:{
            type:String,
            unique:true,//写在index的前面记得，写后面容易不生效
            index:1
        },
        age:Number
    });
    
    //创建一个数据库集合，并将约束Schem附加到集合
    let doterModel = mongoose.model("doter",doterSchema);
    
 
| 注意! 在测试此功能时候，要确保之前的数据库不存在相同name   
---
#  Model对象


## doterModel.find()

     doterModel.find({name: "jugg"},(err,data) => {
            if (!err){
                console.log(data);
             }
     });
     返回结果：数组！
     [ { _id: 59491d649979a83e14605367, name: 'jugg', age: 4556, __v: 0 } ]


## doterModel.findOne()
    
    doterModel.findOne({name: "jugg"},(err,data) => {
            if (!err){
                console.log(data);
             }
     });
     返回结果：对象！
     { _id: 59491d649979a83e14605367, name: 'jugg', age: 4556, __v: 0 }

## doterModel.update()

    doterModel.update({hero:"invoker update"},{nickname:"Kael"}).exec((err,raw) => {
        if (!err) {
            console.log("修改成功",raw);
        }
    });
    返回结果：修改成功 { ok: 1, nModified: 1, n: 1 }
    
    注意：在做数据库修改工作时候，一定要保证数据库之前存在，如果做过删除工作，会返回结果  
    
    修改失败 { ok: 1, nModified: 0, n: 0 }；之前的数据库被删除过！


    
    







## 构建模型Model(Collection)

- 编辑模型

```
var schema = new mongoose.Schema({ name: 'string', size: 'string' });
var Tank = mongoose.model('Tank', schema);

```

- 构建文件

```

//mongoose.model()用来创建模型
var Tank = mongoose.model('Tank', yourSchema);

//"tank",要影射到的集合的名字，字符串
//"yourSchema" 对其进行约束的Schema对象

var small = new Tank({ size: 'small' });
small.save(function (err) {
  if (err) return handleError(err);
  // saved!
})

// or

Tank.create({ size: 'small' }, function (err, small) {
  if (err) return handleError(err);
  // saved!
})

```

- 查询

```
Tank.find({ size: 'small' }).where('createdDate').gt(oneYearAgo).exec(callback);

```

- 删除

```
Tank.remove({ size: 'large' }, function (err) {
  if (err) return handleError(err);
  // removed!
});

```

## document对象
