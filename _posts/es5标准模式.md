---
title: Javascript try catch es5标准模式
date: 2019-05-29 10:47:54
tags: 
- JavaScript 
categories: JavaScript 
description: 
---
## 语法

    
```
//在try里面发生错误，不会执行错误后try里面的代码
    try {
        console.log(a);
        
    } catch (error) {
        alert(error.name+":"+error.message);
    }
```

## error.name对应值的信息

  * EvalError：eval（）的使用与定义不一致
  * RageError：数值越界
  * ReferenceError：非法或不能识别的引用数值
  * SyntaxError：语法解析错误
  * TypeError：操作类型错误
  * URIError：URI处理函数使用不当

##  es5严格模式

发展：es3.0 es5.0 es6.0

默认调用方式：基于es3.0的和es5.0的新增方法

es5.0标准模式：es3.0和5.0的冲突部分用es5.0，否则用es3.0

使用方式:"use strict"

全局模式：在第一行

局部模式：函数第一行




