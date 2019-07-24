---
title: JacaScript arguments
date: 2019-05-29 10:33:47
tags: 
- JavaScript 
categories: JavaScript 
description: 
---
## arguments.callee

指向函数自身引用 
```
var num = (function (n) {
            if (n == 1) {
                return 1;
            }
            return n * arguments.callee(n - 1);
        }(10));
```

立即执行函数执行万就销毁了，所以此处需要用arguments.callee来执行

## func.caller

指向函数的运行环境

```  
function text(){
            demo();
        }
        function demo(){
            //demo的执行环境
            console.log(demo.caller)
        }
        text();
```




