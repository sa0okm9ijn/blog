---
title: JavaScript 实现jquery方法连续调用效果
date: 2019-05-29 11:29:24
tags: 
- JavaScript 
categories: JavaScript 
description: 对象中return this实现方法的连续调用
---
    
```
<script type="text/javascript">
    //实现类似jquery调用方法的连续调用
    var zhang = {
        game:function(){
            console.log("game...");
            return this;
        },
        sleep:function(){
            console.log("sleep...");
            return this;
        },
        watchingLive:function(){
            console.log("watchingLive...");
            return this;
        }
    }
    zhang.game().sleep().watchingLive()
</script>

```

