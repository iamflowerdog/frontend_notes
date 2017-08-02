## children()
### jQuery代码 :

    $("#shareMore").children(".selected");

### 概述:

---


- 用以过滤子元素的表达式；
- 注意：parents()将查找所有祖辈元素，而children()只考虑子元素而不考虑所有后代元素；
- 在每个div中查找.selected 的类；

## hover(over,out)
### 概述

- over:鼠标移到元素上要触发的函数
- out:鼠标移出元素要触发的函数
-------

###### 鼠标悬停的表格加上特定的类

### jQuery代码：

    $("td").hover(
      function () {
        $(this).addClass("hover");
      },
      function () {
        $(this).removeClass("hover");
      }
    );

