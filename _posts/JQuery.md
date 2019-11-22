---
title: JQuery
date: 2019-10-12 16:49:21
tags: 
- JQuery 
categories: JQuery 
description: JQuery基础知识记录
---

# JQuery是什么

jQuery其实就是一堆的js函数(js库)，也是普通的js而已，不是全新的东西，不要畏惧!

# JQuery使用起步

- 线上地址

cdn：http://www.jq22.com/cdn/#a2


- 下载地址

http://www.jq22.com/jquery-info122


- 官方地址

中文:https://www.jquery123.com/
英文原版：https://jquery.com/

- 核心全局函数

$===JQuery

一般用$

- 撸代码从选择开始

`选择元素`

$(); 此函数可以传递多种参数，返回值是对象（jq对象）

`参数亏则`

1. css selector $('.demo')
2. jquery unique selector $(.wrapper ul li:first) 
3. null、undefined 容错机制
4. dom

5. $(function(){})、$(document).ready(function () {})  本质上是一个东西

css selector和context

# JQuery使用-精髓
1. 选择元素
2. 循环操作
3. 链式调用

# 进一步选择元素

## get() 

根据索引返回原生dom 可以接受负数 不传返回所有 

```javascript
$('.demo').get(0)
```

**源码实现原理**

## eq() 

根据索引返回的Jquery对象 可以接受负数

eq()方法和eq()写在选择器中一样，具体使用场合看情况

```javascript
$('demo').eq(0)
```

**源码实现原理**


## find() 

参数和$基本一致 查找元素 在之前基础上查找(效率会高)

```javascript
$('.wrapper').css().find()
```

prevObject 进行这一波操作的时候,前一个JQuery对象

## filter()

参数和$基本一致 


```javascript
$('.wraper ul').find('li').filter(':even')
```

传递函数

```javascript
$('wrapper ul li').filter(function(index,ele){
    return index% 2==0
}).css()
```

## not()

和filter相反


## has()


后代有ul的li元素

```javascript
$('li').has('ul')
```

## is()

返回boolean,是否有交集 is选择里面的是否在前面选择的元素里


点击的元素是否是li
```javascript

$(e.target).is('li')

```

## add()

集中操作

参数和$基本一致 

## end()

回退操作

回退上一个元素对象


**源码实现原理**











## css()

1. 设置样式

**尽量避免写行间样式**

```javascript
$('demo').css({width:'100px'}).css({width:'+=100px'})
```

1. 获取样式

```javascript
$('demo').css('width')
```

## attr

基于setAttribute getAttribute

1. 获取样式
```javascript
$('.demo').attr('class')
```

2. 设置样式
```javascript
$('demo').attr('id','test1')

```

## prop()

特性映射(id name等)  非特性不能映射（自定义属性）

1. 取值
```javascript
$('.demo').prop('checked') 
//返回boolean
```

2. 赋值

```javascript
$('.demo').prop('log',)
```

## html()

返回或设置html结构（string格式） 不支持链式调用

**jquery大部分会集中操作,html取值这里只会操作一个，赋值会集中**

1. 取值
```javascript
//只会获取第一个li元素
$('ul li').html()
```

2. 赋值

```javascript
$('ul').html('<p></p>')


//会设置所有li元素
$('ul li').html('123')
```

3. 传递函数

```javascript

var arrName=['a','b','c']
$('ul li').html(function(index,ele){
   return '';
})

```

## text()

返回或设置纯文本

1. 取值


```javascript
//获取所有li的纯文本
$('ul li').text()
```

2. 赋值

```javascript
//设置所有li
$('ul li').text('123')
```

3. 传递函数

```javascript

var arrName=['a','b','c']
$('ul li').text(function(index,ele){
   return '';
})

```



## size()

相当于js种的length

```javascript
$('ul li').size()
```

## addClass()

添加类名

1. 传递类名
```javascript
$('li').addClass('active duyi')
```

2. 传递函数

```javascript
$('li').addClass(function(index,ele){
    return ''
})
```

## removeClass()

去掉类名

1. 传递类名
```javascript
$('li').removeClass('active duyi')

//全部删除
$('li').removeClass()
```

2. 传递函数

```javascript
$('li').removeClass(function(index,ele){
    return ''
})
```


## hasClass()

判断是不是有类名


```javascript

$('demo').hasClass('active') 返回boolean

```


## val()

针对一些表单元素，获取值

**不会批量取只取一个**

1. 取值$('input[type='checkbox']').val()
```javascript
$('input[type='checkbox']').val()
```

2. 函数方式赋值

```javascript
$('input[type='checkbox']').val(function(index,oldValue){
   return ''
})
```

3. 赋值

```javascript
$('input[type='checkbox']').val('123')
//此处界面上会有变化 取值也会有变化  元素标签上的value并没有变化
```

## serialize()

序列化为字符串

```javascript
$('form').serialize
```

## serializeArray()

序列化未数组

```javascript
$('form').serializeArray()
```


## next()

获取下一个兄弟元素节点,参数限定什么标签

```javascript
$('span').next('').css()
$('span').next('p').css()
```

## prev()

获取上一个兄弟元素节点,参数限定什么标签

```javascript
$('span').prev('').css()
$('span').prev('p').css()
```

## nextAll

获取下面所有兄弟元素节点

```javascript

$(this).nextAll('input[type='checkbox']').prop('checked',true)
$(this).nextAll().prop('checked',true)

```


## prevAll

获取上面所有兄弟元素节点

```javascript

$(this).prevAll('input[type='checkbox']').prop('checked',true)
$(this).prevAll().prop('checked',true)

```

## nextUntil

选取下面的兄弟节点  直到什么为止

```javascript

$(this).nextUntil('h1').prop('checked',true)

//截止到h1 只选取input[type=checkbox]的元素
$(this).nextUntil('h1','input[type=checkbox]').prop

```

## prevUntil

选取上面的兄弟节点  直到什么为止

```javascript

$(this).prevUntil('h1').prop('checked',true)

//截止到h1 只选取input[type=checkbox]的元素
$(this).prevUntil('h1','input[type=checkbox]').prop('checked',true)

```

## siblings

除了自身之外的所有兄弟节点


```javascript
$('li').siblings().css
$('li').siblings('span').css
```

## parent

获取上一级父级元素

```javascript
$(this).parent()

$(this).parent('demo')
```

## parents

获取所有父级元素

```javascript
$(this).parents()

$(this).parents('demo')
```

## closest

离你最近满足条件的父级,从自己开始找，自己满足会返回 需要有参数

```javascript
$('button').closest('button')
```

## offsetParent

最近的有定位的父级

```javascript
$('span').offsetParent()
```

## slice

截取

```javascript
//左闭合右开
$('li').slice(1,5)
```

## insertBefore

剪切操作

链式后续方便操作content

```javascript
//content 插入到box1前面
$('content').insertBefore('.box1')
```

## before

剪切操作
链式后续方便操作box1

```javascript
//box1前面插入content 剪贴
$('.box1').before($('content'))

```

## insertAfter

剪切操作
链式后续方便操作content

```javascript
//content 插入到box1后面
$('content').insertAfter('.box1')
```

## after

剪切操作
链式后续方便操作box1

```javascript
//box1后面插入content 剪贴
$('.box1').after($('content'))

```

## appendTo

相当于appentChild

```javascript
//把content添加到wrappen中
$('conent').appendTo('.wrapper')
```

## append

相当于appentChild

```javascript
//把content添加到wrappen中之后
$('.wrapper').append($('content'))
```

## prepend

```javascript
//把content添加到wrappen中之前
$('.wrapper').prepend($('content'))
```

## prependTo

```javascript
//把content添加到wrappen中之前
$('content').prependTo('.wrapper')
```

## remove

删除之后 在恢复事件没了

```javascript
//剪切
$('div').remove() 
```

## detach

删除之后 事件还在

```javascript
//剪切
$('div').detach() 
```

## $()

相当于document.createElement  凭空创建复杂的html结构

```javascript

$('<div></div>').appendTo($('body'))

```

## wrap

添加父级,给所有元素分别加

1. 普通标签添加
```javascript
$('demo').wrap('<div class='wrapper'></div>')
$('demo').wrap($('<div class='wrapper'></div>'))
$('demo').wrap($('.box')) //赋值一份
```

2. 函数添加


```javascript
$('.demo').wrap(function(index,ele){
    return '<div></div>';
})
```


## wrapInner

给内部元素添加父级

1. 普通标签添加
```javascript

$('demo').wrapInner('<div/>')

```

2. 函数添加

```javascript
$('.demo').wrapInner(function(index,ele){
    return '<div></div>';
})
```

## wrapAll

添加一个统一的父级


```javascript
//给所有demo元素统一的父级 这种需要注意demo必须同级  如果不同级 会参考第一个找到的demo元素
$('demo').wrapAll('<div/>')
```

## unwrap

删除直接父级，最多到body(不包含)

```javascript
$('demo').unwrap()
```

## clone

clone html元素 样式属性都可以克隆过去
事件需要额外的参数


```javascript
$('demo').clone().appendTo('body')

//事件也可以克隆过去

$('demo').clone(true)
```

## data

用来存一些数据 存在jquery上 和dom映射， 不会显示到dom上 但是可以取出来  不操作dom效率会更高

```javascript
$('demo').data('data','a')
$('demo').data({name:'cst'})
```











## on()

绑定系统事件以及自定义事件

1.type 2.selector 3.data 4.handle

1. 2个参数

```javascript
$('.demo').on('click',function(){
   alert('0')
});
```
2. 3个参数

```javascript
$('.demo').on('click',{name:'cst'},function(e){
    console.log(e.data);
})
```

3. 4个参数

```javascript
$('ul').on('click','li',{name:'cst',function(e){

})
```

4. 同时绑定多个事件

```javascript
$('.demo').on({
    click:function(){},
    mouseenter:function(){},
    mouseleave:function(){}
})
```


**源码实现原理**

## one()

1.type 2.selector 3.data 4.handle

只触发一次的事件

## off()

解绑事件

1. 全部解绑
```javascript
$('.demo').off()
```

2. 精准解绑

```javascript
$('demo').off('click')
```

3. 精准解绑函数

```javascript
$('demo').off('click',clickTwo)
```

4. ul li精准解绑

```javascript
$('ul').on('click','li',clickOne)
$('ul').off('click','li',clickOne)
```

## trigger()

主动触发事件

1. 无参数
   
```javascript
$('demo').on('click',function(){})

$('demo').trigger('click')
```

2. 第二个参数

```javascript
$('demo').on('click',function(e,a,b,c,d){})

$('demo').trigger('click',[10,20,30,40])
```

3. 自定义事件的触发

```javascript
$('demo').on('pageLoad',function(){})

$('demo').trigger('pageLoad')
```

**源码实现原理**

## hover()

相当于同时绑定了mouseenter,mouseleave

```javascript

$('.demo').hover(function(){
     //enter
},function(){
    //leave
})

```

## show()

show出来display取决于元素,如果设置过 则还原为设置过的值，没有设置则还原为默认值

显示元素

1. 无参数
```javascript
$(this).show()

```

2. 1个参数

```javascript
//width height opacity padding marging 都在变化
$(this).show(3000)

```

3. 2个参数

swing 运动的变化类型

```javascript
//width height opacity padding marging 都在变化
$(this).show(3000,'swing')

```



## hide()

隐藏元素

1. 无参数
```javascript
$(this).hide()

```

2. 1个参数

```javascript
//width height opacity padding marging 都在变化
$(this).hide(3000)

```

3. 2个参数

swing 运动的变化类型

```javascript
//width height opacity padding marging 都在变化
$(this).hide(3000,'swing')

```

## toggle()

切换状态

```javascript

$('p').on('click',function(){
    
    // if($(this).css('display') == 'one'){
    //     $(this).show()
    // }else{
    //     $(this).hide
    // }

    $(this).toggle()
})

```

## fadeIn()

淡入

```javascript

$('p').on('click',function(){
    
    if($(this).css('display') == 'one'){
        $(this).fadeIn()
    }else{
        $(this).fadeOut()
    }
})

```



## fadeOut()

淡出

```javascript

$('p').on('click',function(){
    
    if($(this).css('display') == 'one'){
        $(this).fadeIn()
    }else{
        $(this).fadeOut()
    }
})

```

## fadeToggle()

切换淡入淡出状态

```javascript

$('p').on('click',function(){
    
    // if($(this).css('display') == 'one'){
    //     $(this).fadeIn()
    // }else{
    //     $(this).fadeOut()
    // }

    $(this).fadeToggle()
})

```

## fadeTo()

变化到那里

多了个0.6 opacity

```javascript

$('p').on('click',function(){
    
    if($(this).css('display') == 'one'){
        $(this).fadeTo(1500,0.6,'swing',function(){
            //over1
        })
    }else{
        $(this).fadeTo(1500,0.1,'swing',function(){
            //over2
        })
    }
})

```


## slideDown()

高度变化

```javascript

$('p').on('click',function(){
    
    if($(this).css('display') == 'one'){
        $(this).slideDown(1500,'swing',function(){
            //over1
        })
    }else{
        $(this).slideUp(1500,'swing',function(){
            //over2
        })
    }
})

```

## slideUp()

高度变化

```javascript

$('p').on('click',function(){
    
    if($(this).css('display') == 'one'){
        $(this).slideDown(1500,'swing',function(){
            //over1
        })
    }else{
        $(this).slideUp(1500,'swing',function(){
            //over2
        })
    }
})

```

## slideToggle()

高度变化

```javascript

$('p').on('click',function(){
    
    // if($(this).css('display') == 'one'){
    //     $(this).slideDown(1500,'swing',function(){
    //         //over1
    //     })
    // }else{
    //     $(this).slideUp(1500,'swing',function(){
    //         //over2
    //     })
    // }
    $(this).slideToggle(1500)
})

```


## animate

1.target 2.duration 3.easing 4.callback

```javascript

$('demo').animate({width:'+=50',left:'+=20'},1000，'swing',function(){
    //over
}).animate({width:'+=50',left:'+=20'},1000，'swing',function(){
    //over
})

```



**源码实现原理**

## stop()

1. 不传参数  停止当前运动 奔向下一个运动

```javascript

$('demo').stop()

```

2. 一个参数 停止所有运动

```javascript

$('demo').stop(true)

```

3. 二个参数 停止当前运动 瞬间运动到当前运动目标点

```javascript

$('demo').stop(true,true)

```




## finish()

直接完成所有运动

```javascript

$('demo').finish()

```

## delay()

运动之间延迟指定毫秒数

```javascript

$('demo').animate({width:'+=50',left:'+=20'},1000，'swing',function(){
    //over
})
.delay(2000)
.animate({width:'+=50',left:'+=20'},1000，'swing',function(){
    //over
})

```




## 关闭jquery所有动画

关闭所有动画 直接到达目标点
```javascript
jQuery.fx.off=true;
```


## 插件jQuery easing pluging

主要增强了easing的类型

https://cdnjs.cloudflare.com/ajax/libs/jquery-easing/1.4.1/jquery.easing.min.js



## quenu()

先进先出

1. 设置队列数据
```javascript

$('.demo').queue('chain',function(){

})
```
2. 获取指定队列名称的数据

```javascript

$('.demo').queue('chain')
```


**源码实现原理**

## dequeue()

1. 从队列中取出数据,原队列大小会减少

```javascript
$('.demo').dequeue('chain')
//只取出一个
```


2. 取一次 后续自动出队

```javascript

$('.demo').queue('chain',function(next){
    console.log('123);
    next()
}.queue('chain',function(next){
    console.log('456');
    next()
})

$('demo').dequeue('chain')
//全部取出
//==>123 456

```

## clearQueue()

//清空队列

```javascript
$('demo').clearQueue()
```

## offset()


返回{left:0,top:0},文档的距离


## position()

返回{left:0,top:0},距离有父级的距离,没有父级取文档

## scrollTop

滚动条滚动的垂直像素

## scrollLeft

滚动条滚动的水平像素

## width/height

content区域

## innerWidth/innerHeight

padding+content区域

## outerWidth/outerHeight

padding+content+border

参数为true的话

padding+content+border+margin

## each()

遍历

```javascript
$('ul li').each(function(index,ele){

})
```

## children()

子元素

```javascript

$('ul').children.each(function(index,ele){

})
```

## index()

获取元素索引

```javascript

$('ul').on('click','li',function(index,ele){
    console.log($(e.target).index));
})
```

筛选

```javascript

$('ul').on('click','li',function(index,ele){
    console.log($(e.target).index($('p span').eq(1)));
})
```






# 工具方法

## $.type()

typeof
undefined string number boolean object function

判断数据类型

```javascript
$.type(undefined)
```

$.type()

undefined string number boolean object function array null date 

## $.isArray()

是否数组

## $.isWindow()

是否时window

## $.isFunction()

是否函数

## $.trim()

```javascript
$.trim('  123  ')
```
去除前后空格


## $.proxy()

改变this指向  类似bind

```javascript

function show(){
    console.log(this)
}

var obj={
    name:'deng',
    age:123
}

var newShow = $.proxy(show,obj);
newShow() //原方法不变 新的方法是改变过的this
```

## $.noConflict()

防止变量命名冲突  

```javascript
$C=$.noConflict()
```

然后就可以用$C了

## $.each()

遍历数组

```javascript

$.each(arr,function(index,ele){

})

```

## $.map()

```javascript
$.map(arr,function(index,ele){
   return ele * index;
})
```

## $.parseJSON

原生js-JSON.parse();

```javascript

var json  = {
    "a":"str",
    "b":"str1"
}

属性名必须是双引号的

$.parseJSON(json)
```

## $.makeArray

1. 传入一个类数组,变成数组  1个参数

```javascript
var obj = {
    0:'a',
    1:'b',
    2:'c',
    length:3
}
$.makeArray(obj);

[].slice.call(obj,0);
```

2. 2个参数,把前面的参数拼接到后面一个参数

```javascript
var obj = {
    0:'a',
    1:'b',
    2:'c',
    length:3
}

var arr=[1,2,3,4]

$.makeArray(arr,obj)

$.makeArray('5',obj)

$.makeArray(obj,arr)
```

## $.extend()

通过它可以把自己定义的函数方法添加到工具方法里面

1. 扩展方法

```javascript

$.extend({
    defineMandom:function(start,final){
        var len = final-start;
        return Math.random*len+start;
    }
})

$.defineMandom(5,10)//调用
```
2. 浅层克隆

```javascript

var obj1={
    lastName:'deng',
    age:6
}

var obj2={
    lastName:'deng',
    age:50,
    smoke:true
}

var obj3={
    lastName:'liu',
    fortune:10000000
}

$.extend(obj1,obj2)//obj2浅层克隆到obj1

$.extend(obj1,obj2,obj3) //2克隆到1  3克隆到1  以最后覆盖为准


```


3. 深层克隆

```javascript

$.extend(true,obj1,obj2,obj3)

```




extend和fn.extend源码区别

```javascript
$.extend=$.fn.extend=function(){
    区别this不一致
}
```


**源码实现原理**

## $.ajax()

向服务器请求一组数据

```javascript

$.ajax({
    url:'',
    type:'GET',
    data:{
        
    },
    success:function(res){

    },
    err:function(e){
        e.status,
        e.statusText,
    },
    complete:function(){
        //不管成功还是失败之后执行的
        //请求完成
    },
    context:$('.wrapper'),//改变this  控制函数的上下文
    timeout:123,//请求延时时间
    async:true,//是否异步
})
```

关于跨域请求的一种方式

```javascript

$.ajax({
    url:'',
    type:'GET',
    datatype:'jsonp', //想要的数据格式，一般不填会智能识别，此处起到跨域作用
    data:{
        wb:'nba',
        cb:'deal'
    },
})
function deal(){

}
```

### 回调地狱

有时候我们可能需要一个请求成功去请求下一个,然后成功再去请求下一个....。这样就会形成了回调地狱

这违反了我们设计模式

设计模式
1. 单一职责原则:一个函数一做一件事
2. 开闭原则:对外扩展开放,对内修改关闭


## $.callback()


1. 不传参数

```javascript

var cb=$.Callbacks();

cb.add(a,b);//添加需要回调的函数

cb.fire();//执行


function a(){
    console.log(a);
}

function b(){
    console.log(b);
}
```

2. 传参数

```javascript

var cb=$.Callbacks('once');//只执行一次


var cb=$.Callbacks('memory');//记忆功能  只要fire过  后续添加的  也会执行

var cb =$.Callbacks('unique');//去重功能 

var cb =$.Callbacks('stopOnFalse');// 遇到返回false的 后面就不知执行了

```

**源码实现原理**

## $.Deferred()

1. 基础用法
   
```javascript
var df = $.Deferred();//延迟对象

//done 成功  // fail  失败   progress 正在进行

//resolve reject notify

//成功
df.done(function(){

});

//失败
df.fail(function(){

})

//正在进行
df.progress(function(){

})


setinterval(function(){
    if(score>90){
        df.resolve()
    }else if(score>80){
        df.reject();
    }else{
        df.notify();
    }
},1500)
```

2. promise

到了现在我们就可以通过状态resolve、reject、notify来触发对应的done、fail、progress了,但是我们在外面也可以执行df.resolve、df.reject、df.notify,这样就违反了正常的处理逻辑,也可以你造成代码异常如下我们优化

```javascript

function createScore(){
    var df = $.Deferred();
    setinterval(function(){
        if(score>90){
            df.resolve()
        }else if(score>80){
            df.reject();
        }else{
            df.notify();
        }
    },1500)
    //这样外面就只能注册done、fail、progress不能触发了
    return df.promise()
}

var df = createScore()
//成功
df.done(function(){

});

//失败
df.fail(function(){

})

//正在进行
df.progress(function(){

})
```

3. then

1. 简化deferred注册的写法

参数对应的分别为done、fail、progress需要执行的函数

```javascript
df.then(function(){
    console.log('done')
},function(){
    console.log('fail')

},function(){
    console.log('progress')
})
```

2. 接力

```javascript
df.then(function(){
    return 'ok';
},function(){
    return 'no';
},function(){
    return 'go on'
}).then(function(param){
    //param=ok
},function(param){
    //param=no
},function(param){
    //param=go on
})
```

3. 返回自定义的deferred

```javascript
df.then(function(){
    var innerDf=$.Deferred();
    setTimeOut(function(){
        innerDf.resolve('自定义成功')
    })
    return innerDf.promise();
}).then(function(params){
   //params  自定义成功
})
```

**源码实现原理**

## $.when

参数可以是一个到多个延迟对象

返回只promise对象

```javascript
$.when(df1,df2,df3).then(function(){
    //3个都成功
},function(){
    //只要一个失败
})
```


# 实例方法

## $.fn.extend()

通过它可以把自己定义的函数方法添加到实例方法里面

1. 扩展方法
```javascript

$.fn.extend({
    drag:function(){
        var diX,disY,self=this;
        $(this).on('mousedown',function(e){
            disX=e.pageX-$(this).offset().left;
            disY=e.pageY-$(this).offset().top;
            $(document).on('mousemove',function(e){
                $(self).css({left:e.pageX-disX,top:e.pageY-disY});
            })
            $(document).on('mouseup',function(e){
                $(document).off('mousemove').off('mouseup');
            })
        })
        return this;
    }
})

$('#demo').drag();//调用

```
2. 浅层克隆
3. 深层克隆

待探究用法

**源码实现原理**


# Jquery插件fullpage编写