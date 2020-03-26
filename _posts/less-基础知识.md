---
title: less-基础知识
date: 2020-01-07 15:00:33
tags:
- css 
categories: css
---

## less

css预处理器

## 嵌套

```less
body{
    margin:0
    padding:0
    .wrapper{
        position:relative;
    }
}
```

## 注释

```css
//注释  只想被开发人员看到
/* 包裹注释*/ 会被编译到文件中
```



## 变量及运算

```less
@color:red;
@w:400px;
@h:@w+100px;
body{
    color:@red
}
```

## 作用域


变量延迟加载  最后依据30px

```less
body{
    @size:15px;
    font-size:@size;
    .wrapper{
        @size:20px;
        font-size:@size;
        @size:30px
    }
}
```

## 混合

```less
.border{
    border:solid 1px #ccc;

}

body{
    .border;
}

带变量和混合


.border(@w,@c){
    border:@w solid @c

}

body{
    .border(1px,#000)
}
```
