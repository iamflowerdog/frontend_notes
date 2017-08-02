#### 关联远端
```
$ git remote add origin https://github.com/iamflowerdog/test.git

```

#### 下载远端

```
$ git pull orgin master
```

#### 推送到远端

```
$ git push -u origin master
```
#### 初始化
```
$ git init
```
#### 创建一个空目录
```
mkdir 创建一个空目录
```
####  创建一个文件
```
touch 创建一个文件
```
#### 查看已经add到工作区的文件

```
git status -s
```
#### 关联多个远端仓库

```
git add remote origin1 URL

git add remote origin2 URL
```

#### 推送多个远端仓库

```
git push -- all 
```

#### 远端和本地冲突解决办法

```
git reset --hard
git pull
```
