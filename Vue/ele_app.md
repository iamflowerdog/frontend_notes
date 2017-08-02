#### 打包入口文件

```
<!--webpack 会把main入口js文件 自动打包注入到body里面 会有个script标签-->
    <!--<script type="text/javascript" src="/app.js"></script></body>-->
```

#### 修改linkActiveClass: 'active'默认类

```
export default new Router({
  linkActiveClass: "active",
  routes: [
    {
      path: '/',
      redirect: '/seller'
    }
```

#### flex布局

- postcss 会自动兼容老版浏览器`-webkit-box-flex: 1;`

```
  .tab
    display flex
    .tab-item
      flex 1
      text-align center
      .active
        color #42b983
```
- flex: 1 , 默认选项
```
flex: 1;
    flex-grow: 1;
    flex-shrink: 1;
    flex-basis: 0%;
```

#### stylus 混合 mixin 处理1像素边框

* 结构化编码

- 语法

```
.tab-item
  width 0
  flex 1
  font-size 14px
  text-align center

  & > a
    display block
    color rgb(77,85,93)
    &.active
      color rgb(240,20,20)
```

- `&.active` 复合选择器 同时选中具有两种类的元素

- 封装

```
border-1px($color)
  position relative
  &:after
    content ''
    display block
    position absolute
    width 100%
    height 1px
    bottom 0
    background-color $color
```

- 调用

```
.tab
    height 40px
    line-height 40px
    display flex
    background-color skyblue
    border-1px(red)
```

- 自适应响应 媒体选择器查询,为tab 添加类 border-1px

```
@media (-webkit-device-pixel-ratio: 2),(min-device-pixel-ratio: 2)
  .border-1px
    &::after
      -webkit-transform transform scaleY(.5)
      transform scaleY(.5)

@media (-webkit-device-pixel-ratio: 3),(min-device-pixel-ratio: 3)
  .border-1px
    &::after
      -webkit-transform transform scaleY(.33333)
      transform scaleY(.33333)
```

#### 垂直对其

- `inline-block` 元素 自身设置 `vertical-align: top` 可以对齐

##### 注意: chorme pc端 最小字体 `font-size: 12px` 移动端 可以比 12px小


#### 文本省略号设置

- 三者缺一不可

```
.bulletin-wrapper
  line-height 28px
  height 28px
  text-overflow ellipsis
  white-space nowrap
  overflow hidden
```

#### 模糊背景

```
.background
  position absolute
  width 100%
  height 100%
  top 0
  left 0
  z-index -1
  filter blur(10px)
```

#### 设置背景图

- 用 `<span class='test'>` 为例，记得给span设置宽高，让他足以显示背景图

```
.icon
    bg-image(decrease_1)
    background-size 16px 16px
    background-repeat no-repeat
    width 16px
    height 16px
    display inline-block
    vertical-align top
```

> 注意： 不要再父容器随便设置 `text-algin: center`