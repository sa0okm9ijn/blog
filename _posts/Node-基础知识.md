---
title: Node-基础知识
date: 2019-12-10 15:01:37
tags:
- JavaScript
- node 
categories: JavaScript
---

## node.js介绍

node.js他是用C++开发的一种运行于服务器端的语言，可以写网站后台程序，可以做服务端应用开发，他的语法就是JAVASCRIPT，会JS，就是会node.js

Node 是一个让 JavaScript 运行在服务端的开发平台，它让 JavaScript 成为与PHP、Python、Perl、Ruby 等服务端语言平起平坐的脚本语言。

Node.js是目前非常火热的技术，但是它的诞生经历却很奇特。

众所周知，在Netscape设计出JavaScript后的短短几个月，JavaScript事实上已经是前端开发的唯一标准。

后来，微软通过IE击败了Netscape后一统桌面，结果几年时间，浏览器毫无进步。（2001年推出的古老的IE 6到今天仍然有人在使用！）

没有竞争就没有发展。微软认为IE6浏览器已经非常完善，几乎没有可改进之处，然后解散了IE6开发团队！而Google却认为支持现代Web应用的新一代浏览器才刚刚起步，尤其是浏览器负责运行JavaScript的引擎性能还可提升10倍。

先是Mozilla借助已壮烈牺牲的Netscape遗产在2002年推出了Firefox浏览器，紧接着Apple于2003年在开源的KHTML浏览器的基础上推出了WebKit内核的Safari浏览器，不过仅限于Mac平台。

随后，Google也开始创建自家的浏览器。他们也看中了WebKit内核，于是基于WebKit内核推出了Chrome浏览器。

Chrome浏览器是跨Windows和Mac平台的，并且，Google认为要运行现代Web应用，浏览器必须有一个性能非常强劲的JavaScript引擎，于是Google自己开发了一个高性能JavaScript引擎，名字叫V8，以BSD许可证开源。

现代浏览器大战让微软的IE浏览器远远地落后了，因为他们解散了最有经验、战斗力最强的浏览器团队！回过头再追赶却发现，支持HTML5的WebKit已经成为手机端的标准了，IE浏览器从此与主流移动端设备绝缘。

浏览器大战和Node有何关系？

话说有个叫Ryan Dahl的歪果仁，他的工作是用C/C++写高性能Web服务。对于高性能，异步IO、事件驱动是基本原则，但是用C/C++写就太痛苦了。于是这位仁兄开始设想用高级语言开发Web服务。他评估了很多种高级语言，发现很多语言虽然同时提供了同步IO和异步IO，但是开发人员一旦用了同步IO，他们就再也懒得写异步IO了，所以，最终，Ryan瞄向了JavaScript。

因为JavaScript是单线程执行，根本不能进行同步IO操作，所以，JavaScript的这一“缺陷”导致了它只能使用异步IO。

选定了开发语言，还要有运行时引擎。这位仁兄曾考虑过自己写一个，不过明智地放弃了，因为V8就是开源的JavaScript引擎。让Google投资去优化V8，咱只负责改造一下拿来用，还不用付钱，这个买卖很划算。

于是在2009年，Ryan正式推出了基于JavaScript语言和V8引擎的开源Web服务器项目，命名为Node.js。虽然名字很土，但是，Node第一次把JavaScript带入到后端服务器开发，加上世界上已经有无数的JavaScript开发人员，所以Node一下子就火了起来。

在Node上运行的JavaScript相比其他后端开发语言有何优势？

最大的优势是借助JavaScript天生的事件驱动机制加V8高性能引擎，使编写高性能Web服务轻而易举。

其次，JavaScript语言本身是完善的函数式语言，在前端开发时，开发人员往往写得比较随意，让人感觉JavaScript就是个“玩具语言”。但是，在Node环境下，通过模块化的JavaScript代码，加上函数式编程，并且无需考虑浏览器兼容性问题，直接使用最新的ECMAScript 6标准，可以完全满足工程上的需求。


``我还听说过io.js，这又是什么鬼``

因为Node.js是开源项目，虽然由社区推动，但幕后一直由Joyent公司资助。由于一群开发者对Joyent公司的策略不满，于2014年从Node.js项目fork出了io.js项目，决定单独发展，但两者实际上是兼容的。

然而中国有句古话，叫做“分久必合，合久必分”。分家后没多久，Joyent公司表示要和解，于是，io.js项目又决定回归Node.js。

具体做法是将来io.js将首先添加新的特性，如果大家测试用得爽，就把新特性加入Node.js。io.js是“尝鲜版”，而Node.js是线上稳定版，相当于Fedora Linux和RHEL的关系。

本章教程的所有代码都在Node.js上调试通过。如果你要尝试io.js也是可以的，不过两者如果遇到一些区别请自行查看io.js的文档。

## 安装node.js

由于Node.js平台是在后端运行JavaScript代码，所以，必须首先在本机安装Node环境。

下载地址https://nodejs.org/en/

在Windows上安装时务必选择全部组件，包括勾选Add to Path。

安装完成,cmd下输入如下,即安装完成

```node.js
node -v
v10.16.3
```

## npm

npm是什么东东？npm其实是Node.js的包管理工具,类似c#的nug等,在安装node的时候已经默认安装好了

以前我的JS，CSS，HTML文件分开写,也没什么问题,可是着前端的发展，社区的壮大，各种前端的库和框架层出不穷，我们项目中可能会使用很多额外的库，如何有效管理这些引入的库文件是一个大问题，而且我们知道基于在HTML中使用``<script>``引入的方式，有两个弊端，一个是会重复引入，二是当库文件数量很多时管理成为一个大难题。面对这样的局面，为了简化开发的复杂度，前端社区涌现了很多实践方法。模块化就是其中一项成功实践,而npm就是这样在node社区中产生的

为啥我们需要一个包管理工具呢？因为我们在Node.js上开发时，会用到很多别人写的JavaScript代码。如果我们要使用别人写的某个包，每次都根据名称搜索一下官方网站，下载代码，解压，再使用，非常繁琐。于是一个集中管理的工具应运而生：大家都把自己开发的模块打包后放到npm官网上，如果要使用，直接通过npm安装就可以直接用，不用管代码存在哪，应该从哪下载。

更重要的是，如果我们要使用模块A，而模块A又依赖于模块B，模块B又依赖于模块X和模块Y，npm可以根据依赖关系，把所有依赖的包都下载下来并管理起来。否则，靠我们自己手动管理，肯定既麻烦又容易出错。

讲了这么多，npm究竟在哪？

其实npm已经在Node.js安装的时候顺带装好了。我们在命令提示符或者终端输入npm -v，应该看到类似的输出：

```
npm -v
6.9.0
```

## js模块化

我们平常的开发中主要用以下几种方式开发,来做到代码的高内聚,低耦合,以及代码的复用、避免变量的命名冲突等问题.

1. 函数
```javascript
function bindEvent(){

}
```
2. 命名空间
```javascript
var obj1={
    a:1,
    b:2
}
```
3. 闭包
```javascript
(function(){
    var a =123;
    function foo(){

    }
    return {foo:foo};
})()
```

4. 模式增强
```javascript
(function($){
    var a =123;
    //$ 模式增强
    function foo(){

    }
    return {foo:foo};
})(jQuery)
```
5. 我们需要的一些特定功能,比如轮播图单独写的js,我们按照一定依赖顺序引入js文件

上面种种都体现了模块化的思想,但是都不完美、不完善,没有一套关于模块化的规范,随着nodejs的出现,有了commonjs规范(模块化的规范),在nodejs里实现了commonjs的规范

模块化的规范主要有commonjs、amd、cmd、es6

### CommonJs

* 每个文件就是一个模块，有自己的作用域。在一个文件里面定义的变量、函数、类，都是私有的，对其他文件不可见。

* CommonJS规范规定，每个模块内部，module变量代表当前模块。这个变量是一个对象，它的exports属性（即module.exports）是对外的接口。加载某个模块，其实是加载该模块的module.exports属性。

* require方法用于加载模块。

* 模块可以多次加载，但是只会在第一次加载时运行一次，然后运行结果就被缓存了，以后再加载，就直接读取缓存结果。要想让模块再次运行，必须清除缓存。

* Node内部提供一个Module构建函数。所有模块都是Module的实例。每个模块内部，都有一个module对象，代表当前模块。

* 如果在命令行下调用某个模块，比如node something.js，那么module.parent就是null。如果是在脚本之中调用，比如require('./something.js')，那么module.parent就是调用它的模块。利用这一点，可以判断当前模块是否为入口脚本。

* 为了方便，Node为每个模块提供一个exports变量，指向module.exports。这等同在每个模块头部，有一行这样的命令。
```javascript
var exports = module.exports;
```
注意，不能直接将exports变量指向一个值，因为这样等于切断了exports与module.exports的联系。
如果你觉得，exports与module.exports之间的区别很难分清，一个简单的处理方法，就是放弃使用exports，只使用module.exports。

示例如下,此处示例为node环境下执行,如果需要在浏览器执行需要工具转化
```javascript
// commonjs/
// |
// +- modules/
// |  |
// |  +- m1.js <-- 模块1
// |  |
// |  +- m2.js <-- 模块2
// |  |
// |  +- m3.js <-- 模块3
// |
// +- index.js <-- 使用koa的js

//m1.js
module.exports = {
    msg: "m1",
    foo: function () {
        return this.msg;
    }
}
//m2.js
module.exports = function(){
    return 'm2';
}
//m3.js
exports.foo = function () {
    return 'm3';
}
//index.js
var m1 = require('./modules/m1');
var m2 = require('./modules/m2');
var m3 = require('./modules/m3');

console.log(m1.foo());
console.log(m2());
console.log(m3.foo());
```


### AMD
CommonJs为服务端而生,采用同步加载方式,因此不适用浏览器端.
AMD规范则是异步加载模块,允许调用指定回调函数

* 使用define定义一个模块,使用require来加载一个模块``define(moduleId,['module1','module2'],function(m1,m2){})``
* 使用依赖require.js
* 依赖前置

```javascript
// commonjs/
// |
// +- libs/
// |  |
// |  +- jquery-3.4.1.min.js <-- jquery
// |  |
// |  +- require.js <-- requery
// +- modules/
// |  |
// |  +- m1.js <-- m1
// |  |
// |  +- m2.js <-- m1
// +- demo.js <-- 使用koa的js
// +- demo.html
//m1.js
define(function () {
    var name = 'm1-amd';

    function getName() {
        return name;
    };
    return {
        getName
    };
})
//m2.js
define(['m1'], function (m1) {
    var msg = 'm2-amd';

    function show() {
        console.log(msg, m1.getName());
    };
    return {
        show
    };
})
//demo.js
(function () {
    require.config({
        paths: {
            m2: './modules/m2',
            m1: './modules/m1',
            jquery: './libs/jquery-3.4.1.min'
        }
    });
    //此处jquery为jquery暴露的名称不可更改
    require(['m2', 'jquery'], function (m2, $) {
        m2.show();
        $('body').css('backgroundColor', '#000');
    })
})()
//demo.html
<script src="./libs/require.js" data-main="./demo.js"></script>
//require.js在加载的时候会检查data-main属性，当加载完毕，data-main属性规定的js文件会第一个被require.js加载并执行
```

### CMD
CMD异步加载,跟AMD的主要区别在于,AMD依赖前置,提前加载依赖.而CMD就近加载,按需加载
* 使用define定义一个模块,使用require来加载一个模块``define(function(require,exports,module){})``
* 使用依赖sea.js
* 就近加载,按需加载

```javascript
// commonjs/
// |
// +- modules/
// |  |
// |  +- m1.js <-- m1
// |  |
// |  +- m2.js <-- m1
// |  |
// |  +- m3.js <-- m1
// |  |
// |  +- m4.js <-- m1
// +- app.js <-- 使用koa的js
// +- index.html
// +- sea.js
//m1.js
define(function (require, exports, module) {
    var msg = "m1";

    function foo() {
        console.log(msg);
    }
    module.exports = {
        foo: foo
    }
})
//m2.js
define(function (require, exports, module) {
    var msg = "m2";

    function bar() {
        console.log(msg);
    }
    module.exports = bar;
})
//m3.js
define(function (require, exports, module) {
    var msg = "m3";

    function foo() {
        console.log(msg);
    }
    exports.m3 = foo;
})
//m4.js
define(function (require, exports, module) {
    var msg = 'm4';
    //同步加载
    var m2 = require('./m2');
    m2();
    //异步加载
    require.async('./m3', function (m3) {
        m3.m3();
    });

    function fun() {
        console.log(msg);
    };
    exports.m4 = fun;
})
//app.js
define(function (require, exports, module) {
    var m1 = require('/modules/m1');
    m1.foo();

    var m4 = require('/modules/m4');
    m4.m4();
})
//index.html
    <script src="./sea.js"></script>
    <script>
        seajs.use('./app.js');
    </script>
```

### Es6
ES6自带模块化,可以使用import引入模块,export导出模块

* 导出
```javascript
//暴漏变量
export var a= '123';
//暴漏函数
export function myFun(){}
//默认暴漏变量函数
export default a='123'
export function myFun(){}
```
* 导入
```javascript
import {m1,m2} from 'lib';
```


## css模块化(预处理器less)

less是一门向后兼容的css扩展语言,是一种动式的语言,属于css预处理语言的一种

### 在浏览器中使用less

在浏览器中使用less,需要less.js的支持,并且必须式http协议打开的网页,文件协议打开的会报错
```html
<link rel="stylesheet/less" type="text/css" href="./index.less">
<script src="//cdnjs.cloudflare.com/ajax/libs/less.js/2.5.3/less.min.js"></script>
```

### 在node中使用less

在node中使用less,即把less文件编译成浏览器支持的css文件,安装less``npm install -g less``,编译``lessc index.less > index.css``,即编译成了浏览器支持的css文件

### less基本语法

* 嵌套
```less
body {
    .wrapper {
        .box {
            width: 100px;
            height: 100px;
            border-bottom: solid 1px red;
        }
    }
}
```
* 变量及变量运算
```less
@color: blue;
@w: 400px;
@h: @w+100px;


.box {
    width: @w;
    height: @h;
    border-bottom: solid 1px @color;
}
```
* 作用域
```less
body {
    @size:10px;
    .wrapper {
        @size:15px;
        .box {
            @size:20px;
            font-size: @size;//输出20px
            width: 100px;
            height: 100px;
            border-bottom: solid 1px red;
        }
    }
}
```
* 作用域的延迟加载
```less
body {
    @size:10px;
    .wrapper {
        @size:15px;
        .box {
            @size:20px;
            font-size: @size;//输出25px
            width: 100px;
            height: 100px;
            @size:25px;
            border-bottom: solid 1px red;
        }
    }
}
```
* 混合 将相同样式抽离 从一个规则引入到另一个规则集的方式
```less
.border{
    border-top: 1px solid red;
    border-bottom:  1px solid blue;
}

body {
    .wrapper {
        width: 200px;
        height: 200px;
        .border;
        .box {
            margin-top: 50px;
            width: 100px;
            height: 100px;
            .border;
        }
    }
}
```
* 混合 带变量及默认值的混合 
```less
.border(@width:5px,@c:#ccc){
    border:@width solid @c;
}

body {
    .wrapper {
        width: 200px;
        height: 200px;
        .border();
        .box {
            margin-top: 50px;
            width: 100px;
            height: 100px;
            .border(3px,#dd0);
        }
    }
}
```
* 模块引入
```less
@import './trangle.less';
```
* arguments
```less
.border(@w,@s,@c){
    border:@arguments;
}

.box{
    width: 200px;
    height: 200px;
    .border(1px,solid,#000);
}
```
* 匹配
```less
.trangle(B, @color, @w) {
    width: 0;
    height: 0;
    border-width: @w;
    border-style: solid;
    border-color: @color transparent transparent transparent;
}

.trangle(T, @color, @w) {
    width: 0;
    height: 0;
    border-width: @w;
    border-style: solid;
    border-color: transparent transparent @color transparent;
}
    .box {
        //匹配
        .trangle(T,blue,40px);
    }
```

## 全局对象和全局变量

因为Node.js是运行在服务区端的JavaScript环境，服务器程序和浏览器程序相比，最大的特点是没有浏览器的安全限制了，而且，服务器程序必须能接收网络请求，读写文件，处理二进制内容，所以，Node.js内置的常用模块就是为了实现基本的服务器功能。这些模块在浏览器环境中是无法被执行的，因为它们的底层代码是用C/C++在Node.js运行环境中实现的。

在前面的JavaScript课程中，我们已经知道，JavaScript有且仅有一个全局对象，在浏览器中，叫window对象。而在Node.js环境中，也有唯一的全局对象，但不叫window，而叫global，这个对象的属性和方法也和浏览器环境的window不同。

* global

表示Node所在的全局环境，类似于浏览器的window对象。需要注意的是，如果在浏览器中声明一个全局变量，实际上是声明了一个全局对象的属性，比如var x = 1等同于设置window.x = 1，但是Node不是这样，至少在模块中不是这样（REPL环境的行为与浏览器一致）。在模块文件中，声明var x = 1，该变量不是global对象的属性，global.x等于undefined。这是因为模块的全局变量都是该模块私有的，其他模块无法取到。

* process

该对象表示Node所处的当前进程，允许开发者与该进程互动。``process === global.process``

* console

指向Node内置的console模块，提供命令行环境中的标准输入、标准输出功能。``console === global.console``


## 异步操作

Node采用V8引擎处理JavaScript脚本，最大特点就是单线程运行，一次只能运行一个任务。这导致Node大量采用异步操作（asynchronous operation），即任务不是马上执行，而是插在任务队列的尾部，等到前面的任务运行完后再执行。

由于这种特性，某一个任务的后续操作，往往采用回调函数（callback）的形式进行定义。

```javascript
console.log("nextTick was set!");

//node退出执行
process.on('exit', function (code) {
    console.log('about to exit with code:' + code);
});

//本轮不执行,等到主线程走完下一轮事件循环才执行

process.nextTick(function () {
    console.log("nextTick callback");
});
=>
nextTick was set!
nextTick callback
about to exit with code:0
```

由于Node环境执行的JavaScript代码是服务器端代码，所以，绝大部分需要在服务器运行期反复执行业务逻辑的代码，必须使用异步代码，否则，同步代码在执行时期，服务器将停止响应，因为JavaScript只有一个执行线程。

服务器启动时如果需要读取配置文件，或者结束时需要写入到状态文件时，可以使用同步代码，因为这些代码只在启动和结束时执行一次，不影响服务器正常运行时的异步执行。


## js执行环境判断

```javascript

if (typeof(window) === 'undefined') {
    console.log('node.js');
} else {
    console.log('browser');
}

```

## 基本模块

### fs模块

* 读文件
```javascript
var fs = require('fs');
fs.readFile('sample.txt', 'utf-8', function (err, data) {
    if (err) {
        console.log(err);
    } else {
        console.log(data);
    }
});
```

* 写文件
```javascript
var fs = require('fs');
var data = 'Hello,Node.js';
fs.writeFile('output.txt', data, function (err) {
    if (err) {
        console.log(err);
    } else {
        console.log('ok');
    }
})
```

* 获取文件信息
```javascript
var fs = require('fs');
fs.stat('sample.txt', function (err, stat) {
    if (err) {
        console.log(txt);
    } else {
        console.log('isFile:' + stat.isFile());
        console.log('isDirectory' + stat.isDirectory());
        if (stat.isFile()) {
            console.log('size:' + stat.size);
            console.log('birth time' + stat.birthtime);
            console.log('modified time' + stat.mtime);
        }
    }
})
```
上述都属异步的方式获取,同步都是加Async,如``fs.writeFileSync``


* 读流
```javascript
var fs= require('fs');
//打开一个流
var rs = fs.createReadStream('resources/sample.txt','utf-8');
//开始读取流
rs.on('data',function(chunk){
    console.log('DATA:');
    console.log(chunk);
});
//读取结束
rs.on('end',function(){
    console.log('end');
});
//读取有异常
rs.on('error',function(err){
    console.log('ERROR'+err)
});
```

* 写流
```javascript
var ws1=fs.createWriteStream('resources/output1.txt','utf-8');

ws1.write('使用stream写入文本数据...\n');
ws1.write('END.');
ws1.end();

var ws2=fs.createWriteStream('resources/output2.txt');
ws2.write(new Buffer('使用Stream写入二进制数据...\n','utf-8'));
ws2.write(new Buffer('END.','utf-8'));
ws2.end();

```
* pipe 
就像可以把两个水管串成一个更长的水管一样，两个流也可以串起来。一个Readable流和一个Writable流串起来后，所有的数据自动从Readable流进入Writable流，这种操作叫pipe。
```javascript
var rs=fs.createReadStream('resources/sample.txt');
var ws= fs.createWriteStream('resources/copied.txt');
rs.pipe(ws);
```

### http模块

```javascript
//文件服务器
var fs = require('fs');
var url = require('url');
var path = require('path');
var http = require('http');

//解析为当前目录
var root = path.resolve(process.argv[2] || '.');
var server = http.createServer(function (request, response) {
    var pathname = url.parse(request.url).pathname;
    var filepath = path.join(root, pathname);
    fs.stat(filepath, function (err, stats) {
        if (!err && stats.isFile()) {
            console.log('200' + request.url);
            response.writeHead(200,{"Content-Type":"application/jaContent-Typevascript; charset=utf-8"});
            //将文件流导向response;
            fs.createReadStream(filepath, 'utf-8').pipe(response);
        } else {
            response.writeHead(404);
            response.end('404 Not Found');
        }
    })
});
server.listen(8090);
console.log('Server is running at http://127.0.0.1:8090/');
```

我们访问根目录下的文件时候就会看到文件里面的内容,这里我访问的是js文件,所有设置了content-type如果是html,可自行设置

### crypto模块

* MD5
MD5是一种常用的哈希算法，用于给任意数据一个“签名”。这个签名通常用一个十六进制的字符串表示
```javascript
var crypto = require('crypto');
var hash = crypto.createHash('md5');
hash.update('admin');
console.log('MD:'+hash.digest('hex'));  
```
* sha1
```javascript
var sha1 = crypto.createHash('sha1');
sha1.update('admin');
console.log('sha1:' + sha1.digest("hex"));
```
* Hmac
Hmac算法也是一种哈希算法，它可以利用MD5或SHA1等哈希算法。不同的是，Hmac还需要一个密钥：
```javascript
var hmac = crypto.createHmac('md5', 'secret-key');
hmac.update('admin');
console.log('Hmac:' + hmac.digest('hex'));
```
* AES
AES是一种常用的对称加密算法，加解密都用同一个密钥。crypto模块提供了AES支持，但是需要自己封装好函数，便于使用
```javascript
function aesEncrypt(data, key) {
    var cipher = crypto.createCipheriv('aes192', key, '1111111111111111');
    var cryted = cipher.update(data, 'utf8', 'hex');
    cryted += cipher.final('hex');
    return cryted;
}

function aesDecrypt(encrypted, key) {
    var decipher = crypto.createDecipheriv('aes192', key, '1111111111111111');
    var descypted = decipher.update(encrypted, 'hex', 'utf8');
    descypted += decipher.final('utf8');
    return descypted;
}

var data = 'hello,this is a secret message';
var key = '111111111111111111111111';

var encrypted = aesEncrypt(data, key);
var decrypted = aesDecrypt(encrypted, key);

console.log('Plain text' + data);
console.log('aes Encrypted text' + encrypted);
console.log('aes encrypted text' + decrypted);
```
* diffie-hellman
DH算法是一种密钥交换协议，它可以让双方在不泄漏密钥的情况下协商出一个密钥来。搞不懂啥意思,先记下来
```javascript
var primeLength = 1024; // 素数p的长度
var generator = 5; // 素数a

// 创建客户端的DH实例
var client = crypto.createDiffieHellman(primeLength, generator);
// 产生公、私钥对，Ya = a^Xa mod p
var clientKey = client.generateKeys();

// 创建服务端的DH实例，采用跟客户端相同的素数a、p
var server = crypto.createDiffieHellman(client.getPrime(), client.getGenerator());
// 产生公、私钥对，Yb = a^Xb mod p
var serverKey = server.generateKeys();

// 计算 Ka = Yb^Xa mod p
var clientSecret = client.computeSecret(server.getPublicKey());
// 计算 Kb = Ya^Xb mod p
var serverSecret = server.computeSecret(client.getPublicKey());

// 由于素数p是动态生成的，所以每次打印都不一样
// 但是 clientSecret === serverSecret
console.log(clientSecret.toString('hex'));
console.log(serverSecret.toString('hex'));
```
* RSA
RSA算法是一种非对称加密算法，即由一个私钥和一个公钥构成的密钥对，通过私钥加密，公钥解密，或者通过公钥加密，私钥解密。其中，公钥可以公开，私钥必须保密。
```javascript
var fs = require('fs');
var crypto=require('crypto');

function loadkey(file){
    return fs.readFileSync(file,'utf8');
}

var prvkey = loadkey('./rsa-prv.pem');
var pubkey = loadkey('./rsa-pub.pem');
var message='hello world';

// 使用私钥加密
var enc_by_prv = crypto.privateEncrypt(prvkey,Buffer.from(message,'utf8'));
console.log('私钥加密 '+enc_by_prv.toString('hex'));

// 使用公钥解密
var dec_by_pub = crypto.publicDecrypt(pubkey,enc_by_prv);
console.log('公钥解密'+dec_by_pub.toString('utf8'))


// 使用公钥加密
var enc_by_pub = crypto.publicEncrypt(pubkey,Buffer.from(message,'utf8'));
console.log('公钥加密'+enc_by_pub.toString('hex'));

// 使用私钥解密
var dec_by_prv = crypto.privateDecrypt(prvkey,enc_by_pub);
console.log('私钥解密'+dec_by_prv.toString('utf8'));
```


## Web开发

由于Node.js把JavaScript引入了服务器端,因此，原来必须使用PHP/Java/C#/Python/Ruby等其他语言来开发服务器端程序，现在可以使用Node.js开发了！
在Node.js诞生后的短短几年里，出现了无数种Web框架、ORM框架、模版引擎、测试框架、自动化构建工具，数量之多

### koa Web框架

koa是Express的下一代基于Node.js的web框架，目前有1.x和2.0两个版本。
 
* 历史
1. Express
Express是第一代最流行的web框架，它对Node.js的http进行了封装，用起来如下：
```javascript
var express = require('express');
var app=express();
app.get('/',function(req,res){
    res.send('hello world');
})

app.listen(3000,function(){
    console.log('Example app listen on port 3000');
})
```
虽然Express的API很简单，但是它是基于ES5的语法，要实现异步代码，只有一个方法：回调。如果异步嵌套层次过多，代码写起来就非常难看：

2. koa 1.0
随着新版Node.js开始支持ES6，Express的团队又基于ES6的generator重新编写了下一代web框架koa。和Express相比，koa 1.0使用generator实现异步，代码看起来像同步的：

3. koa 2.0
koa团队并没有止步于koa 1.0，他们非常超前地基于ES7开发了koa2，和koa 1相比，koa2完全使用Promise并配合async来实现异步。

本教程将使用教程将使用最新的koa2开发！


#### 创建Koa工程

```javascript
// 导入koa，和koa 1.x不同，在koa2中，我们导入的是一个class，因此用大写的Koa表示:
const Koa = require('koa');

// 创建一个Koa对象表示web app本身:
const app = new Koa();

// 对于任何请求，app将调用该异步函数处理请求：
app.use(async(ctx,next)=>{
    await next();
    ctx.response.type='text/html';
    ctx.response.body='<h1>hello,koa2</h1>'
});

app.listen(3000);
console.log('app started at port 3000...');

```

打卡浏览器访问http://localhost:3000;


``koa middleware``

koa把很多async函数组成一个处理链，每个async函数都可以做一些自己的事情，然后用await next()来调用下一个async函数。我们把每个async函数称为middleware，这些middleware可以组合起来，完成很多有用的功能。

如下面3个middleware组成处理链，依次打印日志，记录处理时间，输出HTML：

```javascript
var Koa = require('koa');

var app = new Koa();

app.use(async (ctx, next) => {
    console.log(`${ctx.request.method} ${ctx.request.url}`);
    await next(); //调用下一个middleware
});

app.use(async (ctx, next) => {
    var start = new Date().getTime();
    await next(); //调用下一个middleware
    var ms = new Date().getTime() - start;
    console.log(`time:${ms}ms`);
});

app.use(async (ctx, next) => {
    await next();
    ctx.response.type = 'text/html';
    ctx.response.body = '<h1>Hello,koa2</h1>'
});

app.listen(3000);
```

middleware的顺序很重要，也就是调用app.use()的顺序决定了middleware的顺序。

此外，如果一个middleware没有调用await next()，会怎么办？答案是后续的middleware将不再执行了。

#### 处理url

在hello-koa工程中，我们处理http请求一律返回相同的HTML，这样虽然非常简单，但是用浏览器一测，随便输入任何URL都会返回相同的网页。

正常情况下，我们应该对不同的URL调用不同的处理函数


应该有一个能集中处理URL的middleware，它根据不同的URL调用不同的处理函数，这样，我们才能专心为每个URL编写处理函数。

* koa-router get请求
```javascript
//get请求
var Koa = require('koa');
//注意require('koa-router')返回的是函数
var router = require('koa-router')();

var app = new Koa();


// log request URL;
app.use(async (ctx, next) => {
    console.log(`Process ${ctx.request.method} ${ctx.request.url}...`);
    await next();
});

// add  url-route

router.get('/hello/:name', async (ctx, next) => {
    var name = ctx.params.name;
    ctx.response.body = `<h1>hello,${name}</h1>`;
});

router.get('/',async(ctx,next)=>{
    ctx.response.body=`<h1>Index</h1>`;
});

app.use(router.routes());

app.listen(3000);
console.log('app started at port 3000');


```

用post请求处理URL时，我们会遇到一个问题：post请求通常会发送一个表单，或者JSON，它作为request的body发送，但无论是Node.js提供的原始request对象，还是koa提供的request对象，都不提供解析request的body的功能！

所以，我们又需要引入另一个middleware来解析原始request请求，然后，把解析后的参数，绑定到ctx.request.body中。

koa-bodyparser就是用来干这个活的。

* koa-router post请求
```javascript
//post请求
var Koa = require('koa');
//注意require('koa-router')返回的是函数
var router = require('koa-router')();

var bodyParser=require('koa-bodyParser');

var app = new Koa();

// log request URL;
app.use(async (ctx, next) => {
    console.log(`Process ${ctx.request.method} ${ctx.request.url}...`);
    await next();
});

router.get('/',async(ctx,next)=>{
    ctx.response.body=`<h1>Index</h1>
            <form action="/sigin" method='post'>
                <p>Name:<input name="name" value="koa"/></p>
                <p>Password:<input name="password" type="password"/></p>
                <p><input type="submit"value="Submit"/></p>
            </form>`;
});

router.post('/sigin',async(ctx,next)=>{
    var name=ctx.request.body.name||'';
    var password=ctx.request.body.password||'';
    console.log(`signin with name:${name},password:${password}`);
    if(name === 'koa' && password==='12345'){
        ctx.response.body=`<h1>welcome:${name}!</h1>`
    }else{
        ctx.response.body=`<h1>Login field</h1>
            <p><a href='/'>Try again</a></p>`;
    }
});


app.use(bodyParser());
app.use(router.routes());

app.listen(3000);
console.log('app started at port 3000');
```
所有的URL处理函数都放到app.js里显得很乱，而且，每加一个URL，就需要修改app.js。随着URL越来越多，app.js就会越来越长。

如果能把URL处理函数集中到某个js文件，或者某几个js文件中就好了，然后让app.js自动导入所有处理URL的函数。这样，代码一分离，逻辑就显得清楚了。




* 重构
```javascript
// url2-koa/
// |
// +- controllers/
// |  |
// |  +- hello.js <-- 处理login相关URL
// |  |
// |  +- index.js <-- 处理用户管理相关URL
// |
// +- app.js <-- 使用koa的js
// |
// +- controller.js <-- 自动处理url函数js
// |
// +- package.json <-- 项目描述文件
// |
// +- node_modules/ <-- npm安装的所有依赖包

//hello.js

var fn_hello = async (ctx, next) => {
    var name = ctx.params.name;
    ctx.response.body = `<h1>Hello, ${name}!</h1>`;
};

module.exports = {
    'GET /hello/:name': fn_hello
};

//index.js
var fn_index = async (ctx, next) => {
    ctx.response.body = `<h1>Index</h1>
        <form action="/signin" method="post">
            <p>Name: <input name="name" value="koa"></p>
            <p>Password: <input name="password" type="password"></p>
            <p><input type="submit" value="Submit"></p>
        </form>`;
};

var fn_signin = async (ctx, next) => {
    var name = ctx.request.body.name || '';
    var password = ctx.request.body.password || '';
    console.log(`signin with name: ${name}, password: ${password}`);
    if (name === 'koa' && password === '12345') {
        ctx.response.body = `<h1>Welcome, ${name}!</h1>`;
    } else {
        ctx.response.body = `<h1>Login failed!</h1>
        <p><a href="/">Try again</a></p>`;
    }
};

module.exports={
    'GET /':fn_index,
    'POST /signin':fn_signin
}

//controller.js


// 先导入fs模块，然后用readdirSync列出文件
// 这里可以用sync是因为启动时只运行一次，不存在性能问题:
var fs = require('fs');

function addMapping(router, mapping) {
    for (var url in mapping) {
        if (url.startsWith('GET ')) {
            var path = url.substring(4);
            router.get(path, mapping[url]);
            console.log(`register URL mapping: GET ${path}`);
        } else if (url.startsWith('POST ')) {
            var path = url.substring(5);
            router.post(path, mapping[url]);
            console.log(`register URL mapping: POST ${path}`);
        } else {
            console.log(`invalid URL: ${url}`);
        }
    }
}

function addControllers(router) {
    var files = fs.readdirSync(__dirname + '/controllers');
    var js_files = files.filter((f) => {
        return f.endsWith('.js');
    });

    for (var f of js_files) {
        console.log(`process controller: ${f}...`);
        let mapping = require(__dirname + '/controllers/' + f);
        addMapping(router, mapping);
    }
}


module.exports = function (dir) {
    var controllers_dir = dir || 'controllers'; // 如果不传参数，扫描目录默认为'controllers'
    var router = require('koa-router')();
    addControllers(router, controllers_dir);
    return router.routes();
}

//app.js


var Koa=require('koa');

var app = new Koa();

var bodyParser=require('koa-bodyParser');

// 导入controller middleware:
var controller = require('./controller');


app.use(bodyParser());
app.use(controller());

app.listen(3000);

```







#### 使用Nunjucks

Nunjucks是什么东东？其实它是一个模板引擎。
那什么是模板引擎？
模板引擎就是基于模板配合数据构造出字符串输出的一个组件。比如下面的函数就是一个模板引擎：

```javascript
function examResult (data) {
    return `${data.name}同学一年级期末考试语文${data.chinese}分，数学${data.math}分，位于年级第${data.ranking}名。`
}
```

如果我们输入数据如下：

```javascript
examResult({
    name: '小明',
    chinese: 78,
    math: 87,
    ranking: 999
});
```

该模板引擎把模板字符串里面对应的变量替换以后，就可以得到以下输出：
```
小明同学一年级期末考试语文78分，数学87分，位于年级第999名。
```

模板引擎最常见的输出就是输出网页，也就是HTML文本。

输出HTML有几个特别重要的问题需要考虑：JavaScript的模板字符串实现起来非常困难

* 转义
对特殊字符要转义，避免受到XSS攻击。比如，如果变量name的值不是小明，而是小明<script>...</script>，模板引擎输出的HTML到了浏览器，就会自动执行恶意JavaScript代码。
* 格式化
对不同类型的变量要格式化，比如，货币需要变成12,345.00这样的格式，日期需要变成2016-01-01这样的格式。
* 简单逻辑
```
{{ name }}同学，
{% if score >= 90 %}
    成绩优秀，应该奖励
{% elif score >=60 %}
    成绩良好，继续努力
{% else %}
    不及格，建议回家打屁股
{% endif %}
```

所以，我们需要一个功能强大的模板引擎，来完成页面输出的功能。


我们选择Nunjucks作为模板引擎。Nunjucks是Mozilla开发的一个纯JavaScript编写的模板引擎，既可以用在Node环境下，又可以运行在浏览器端。但是，主要还是运行在Node环境下，因为浏览器端有更好的模板解决方案，例如MVVM框架。

如果你使用过Python的模板引擎jinja2，那么使用Nunjucks就非常简单，两者的语法几乎是一模一样的，因为Nunjucks就是用JavaScript重新实现了jinjia2。

* 基本渲染
```javascript
// use-nunjucks/
// |
// +- views/
// |  |
// |  +- hello.html <-- 处理login相关URL
// |  |
// +- app.js <-- 使用koa的js
// +- package.json <-- 项目描述文件
// |
// +- node_modules/ <-- npm安装的所有依赖包

//hello.html

// <h1>hello {{name}}</h1>


//简单的渲染 app.js
var nunjucks = require('nunjucks');

function createEnv(path, opts) {
    var autoescape = opts.autoescape === undefined ? true : opts.autoescape;
    var noCache = opts.noCache || false;
    var watch = opts.watch | false;
    var throwOnUndefined = opts.throwOnUndefined || false;
    var env = new nunjucks.Environment(
        new nunjucks.FileSystemLoader(path, {
            noCache: noCache,
            watch: watch
        }), {
            autoescape: autoescape,
            throwOnUndefined: throwOnUndefined
        }
    )
    return env;
};
var env = createEnv('views', {
    watch: true,
});

var s = env.render('hello.html', {
    name: '小明1'
});
console.log(s);
```

* 继承
```javascript
// use-nunjucks/
// |
// +- views/
// |  |
// |  +- base.html
// |  +- extend.html
// |
// +- app.js <-- 使用koa的js
// +- package.json <-- 项目描述文件
// |
// +- node_modules/ <-- npm安装的所有依赖包

//base.html
// <!DOCTYPE html>
// <html lang="en">
// <head>
//     <meta charset="UTF-8">
//     <meta name="viewport" content="width=device-width, initial-scale=1.0">
//     <meta http-equiv="X-UA-Compatible" content="ie=edge">
//     <title>Document</title>
// </head>
// <body>
//     {% block header %}<h3>Unnamed</h3>{% endblock  %}
//     {% block body %}<div>No body</div>{% endblock  %}
//     {% block footer%}<div>copyright</div>{% endblock  %}    
// </body>
// </html>

//extend.html

// {% extends 'base.html' %}
// {% block header%}<h1>{{header}}</h1>{% endblock  %}
// {% block body%}<p>{{body}}</p>{% endblock %}


//app.js

console.log(env.render('extend.html',{
    header:'hello',
    body:'bla la la...'
}));
```

* 性能
对于模板渲染本身来说，速度是非常非常快的，因为就是拼字符串嘛，纯CPU操作。
性能问题主要出现在从文件读取模板内容这一步。这是一个IO操作，在Node.js环境中，我们知道，单线程的JavaScript最不能忍受的就是同步IO，但Nunjucks默认就使用同步IO读取模板文件。
好消息是Nunjucks会缓存已读取的文件内容，也就是说，模板文件最多读取一次，就会放在内存中，后面的请求是不会再次读取文件的，只要我们指定了noCache: false这个参数。
在开发环境下，可以关闭cache，这样每次重新加载模板，便于实时修改模板。在生产环境下，一定要打开cache，这样就不会有性能问题。

#### MVC

我们已经可以用koa处理不同的URL，还可以用Nunjucks渲染模板。现在，是时候把这两者结合起来了！
这就是传说中的MVC：Model-View-Controller，中文名“模型-视图-控制器”。

* 异步函数是C：Controller，Controller负责业务逻辑，比如检查用户名是否存在，取出用户信息等等；
* 包含变量{{ name }}的模板就是V：View，View负责显示逻辑，通过简单地替换一些变量，View最终输出的就是用户看到的HTML。
* Model就是一个JavaScript对象：
```javascript
{ name: 'Michael' }
```

工程view-koa结构如下：
```
view-koa/
|
+- controllers/ <-- Controller
|
| +- index.js
| +- signin.js
+- views/ <-- html模板文件
|
+- static/ <-- 静态资源文件
|
+- controller.js <-- 扫描注册Controller
|
+- static-files.js
|
+- templating.js
|
+- app.js <-- 使用koa的js
|
+- package.json <-- 项目描述文件
|
+- node_modules/ <-- npm安装的所有依赖包
```

这里只列出主要代码部分,静态资源文件和html文件自己补充即可

```javascript
//index.js
module.exports = {
    'GET /': async (ctx, next) => {
        ctx.render('index.html', {
            title: 'welcome'
        });
    }
}
//signin.js
module.exports = {
    'POST /signin': async (ctx, next) => {
        var email = ctx.request.body.email || '';
        var password = ctx.request.body.password || '';
        if (email === 'admin@example.com' && password === '123456') {
            ctx.render('signin-ok.html', {
                title: 'Sign In Ok',
                name: 'Mr Node'
            });
        } else {
            ctx.render('signin-failed.html', {
                title: 'Sign In Failed'
            });
        }
    }
}
//app.js

var Koa=require('koa');

var app = new Koa();

var bodyParser=require('koa-bodyParser');

// 导入controller middleware:
var controller = require('./controller');

var staticFiles = require('./static-files');

var templating = require('./templating');

const isProduction = process.env.NODE_ENV === 'production';
app.use(staticFiles('/static/', __dirname + '/static'));
app.use(bodyParser());
app.use(templating('views', {
    noCache: !isProduction,
    watch: !isProduction
}));
app.use(controller());
app.listen(3000);

//controller.js


// 先导入fs模块，然后用readdirSync列出文件
// 这里可以用sync是因为启动时只运行一次，不存在性能问题:
var fs = require('fs');

function addMapping(router, mapping) {
    for (var url in mapping) {
        if (url.startsWith('GET ')) {
            var path = url.substring(4);
            router.get(path, mapping[url]);
            console.log(`register URL mapping: GET ${path}`);
        } else if (url.startsWith('POST ')) {
            var path = url.substring(5);
            router.post(path, mapping[url]);
            console.log(`register URL mapping: POST ${path}`);
        } else {
            console.log(`invalid URL: ${url}`);
        }
    }
}

function addControllers(router) {
    var files = fs.readdirSync(__dirname + '/controllers');
    var js_files = files.filter((f) => {
        return f.endsWith('.js');
    });

    for (var f of js_files) {
        console.log(`process controller: ${f}...`);
        console.log(__dirname + '/controllers/' + f);
        let mapping = require(__dirname + '/controllers/' + f);
       
        addMapping(router, mapping);
    }
}


module.exports = function (dir) {
    var controllers_dir = dir || 'controllers'; // 如果不传参数，扫描目录默认为'controllers'
    var router = require('koa-router')();
    addControllers(router, controllers_dir);
    return router.routes();
}
//static-files.js
var path = require('path');
var mime = require('mime');
var fs = require('mz/fs');

// url: 类似 '/static/'
// dir: 类似 __dirname + '/static'
function staticFiles(url, dir) {
    return async (ctx, next) => {
        var rpath = ctx.request.path;
        if (rpath.startsWith(url)) {
            var fp = path.join(dir, rpath.substring(url.length));
            if (await fs.exists(fp)) {
                ctx.response.type = mime.lookup(rpath);
                ctx.response.body = await fs.readFile(fp);
            } else {
                ctx.response.status = 404;
            }
        } else {
            await next();
        }
    };
}

module.exports = staticFiles;

//templating.js
var nunjucks = require('nunjucks');

function createEnv(path, opts) {
    var
        autoescape = opts.autoescape === undefined ? true : opts.autoescape,
        noCache = opts.noCache || false,
        watch = opts.watch || false,
        throwOnUndefined = opts.throwOnUndefined || false,
        env = new nunjucks.Environment(
            new nunjucks.FileSystemLoader(path || 'views', {
                noCache: noCache,
                watch: watch,
            }), {
                autoescape: autoescape,
                throwOnUndefined: throwOnUndefined
            });
    return env;
}

function templating(path, opts) {
    var env = createEnv(path, opts);
    return async (ctx, next) => {
        ctx.render = function (view, model) {
            // 把render后的内容赋值给response.body:
            ctx.response.body = env.render(view, Object.assign({}, ctx.state || {}, model || {}));
            // 设置Content-Type:
            ctx.response.type = 'text/html';
        };
        // 继续处理请求:
        await next();
    }
}
module.exports = templating;
```

### mysql

#### Sequelize

Node的ORM框架Sequelize,依赖驱动mysql

* 配置数据库相关配置
```javascript
//config.js
var config = {
    database: 'test', // 使用哪个数据库
    username: 'root', // 用户名
    password: '123', // 口令
    host: 'localhost', // 主机名
    port: 3306 // 端口号，MySQL默认3306
};

module.exports = config;
```

* 初始化一个实例
```javascript
const Sequelize = require('sequelize');
const config = require('./config');

var sequelize = new Sequelize(config.database, config.username, config.password, {
    host: config.host,
    dialect: 'mysql',
    pool: {
        max: 5,
        min: 0,
        idle: 30000
    }
});
```
* 定义模型,映射数据库表(此时的数据库应该存在一张表)
```javascript
var Pet = sequelize.define('pet', {
    id: {
        type: Sequelize.STRING(50),
        primaryKey: true
    },
    name: Sequelize.STRING(100),
    gender: Sequelize.BOOLEAN,
    birth: Sequelize.STRING(10),
    createdAt: Sequelize.BIGINT,
    updatedAt: Sequelize.BIGINT,
    version: Sequelize.BIGINT
}, {
    timestamps: false
});
```
* 实现增删改查
```javascript
// //创建
(async () => {
    var dog = await Pet.create({
        id: 'd-' + now,
        name: 'Odie',
        gender: false,
        birth: '2008-08-08',
        createdAt: now,
        updatedAt: now,
        version: 0
    });
    console.log('created: ' + JSON.stringify(dog));
})();
//查询
(async () => {
    var pets = await Pet.findAll({
        where: {
            name: 'Gaffey'
        }
    });
    console.log(`find ${pets.length} pets:`);
    for (let p of pets) {
        console.log(JSON.stringify(p));
    }
})();

//修改
(async () => {
    var pets = await Pet.findAll({
        where: {
            name: 'Gaffey'
        }
    });
    pets.gender=true;
    pets[0].save();
})();

//删除数据
(async () => {
    var pets = await Pet.findAll({
        where: {
            name: 'Gaffey'
        }
    });
    await pets[0].destroy();
})();
```

#### 规范化Model

一个大型Web App通常都有几十个映射表，一个映射表就是一个Model。如果按照各自喜好，那业务代码就不好写。Model不统一，很多代码也无法复用。
所以我们需要一个统一的模型，强迫所有Model都遵守同一个规范，这样不但实现简单，而且容易统一风格。
* 统一主键，名称必须是id，类型必须是STRING(50)；
* 主键可以自己指定，也可以由框架自动生成（如果为null或undefined）；
* 所有字段默认为NOT NULL，除非显式指定；
* 统一timestamp机制，每个Model必须有createdAt、updatedAt和version，分别记录创建时间、修改时间和版本号。其中，createdAt和updatedAt以BIGINT存储时间戳，最大的好处是无需处理时区，排序方便。version每次修改时自增。

```javascript
// model-sequelize/
// |
// +- .vscode/
// |  |
// |  +- launch.json <-- VSCode 配置文件
// |
// +- models/ <-- 存放所有Model
// |  |
// |  +- Pet.js <-- Pet
// |  |
// |  +- User.js <-- User
// |
// +- config.js <-- 配置文件入口
// |
// +- config-override.js <-- 默认配置文件
// |
// +- config-default.js <-- 默认配置文件
// |
// +- config-test.js <-- 测试配置文件
// |
// +- db.js <-- 如何定义Model
// |
// +- model.js <-- 如何导入Model
// |
// +- init-db.js <-- 初始化数据库
// |
// +- app.js <-- 业务代码
// |
// +- package.json <-- 项目描述文件
// |
// +- node_modules/ <-- npm安装的所有依赖包

//db.js
var Sequelize = require('sequelize');
var uuid = require('uuid');

var config = require('./config');

console.log(`init sequelize...`);

function generateId() {
    return uuid.v4();
}

var sequelize = new Sequelize(config.database, config.username, config.password, {
    host: config.host,
    dialect: config.dialect,
    pool: {
        max: 5,
        min: 0,
        idle: 10000
    }
});
var ID_TYPE = Sequelize.STRING(50);

function defineModel(name, attributes) {
    var attrs = {};
    for (var key in attributes) {
        var value = attributes[key];
        if (typeof (value) == 'object' && value['type']) {
            value.allowNull = value.allowNull || false;
            attrs[key] = value;
        } else {
            attrs[key] = {
                type: value,
                allowNull: false,
            }
        }
    };
    attrs.id = {
        type: ID_TYPE,
        primaryKey: true
    };
    attrs.createAt = {
        type: Sequelize.BIGINT,
        allowNull: false,
    };
    attrs.updateAt = {
        type: Sequelize.BIGINT,
        allowNull: false,
    };
    attrs.version = {
        type: Sequelize.BIGINT,
        allowNull: false,
    };
    return sequelize.define(name, attrs, {
        tablename: name,
        timestams: false,
        hooks: {
            beforeValidate: function (obj) {
                var now = Date.now();
                if (obj.isNewRecord) {
                    console.log('will create entity...' + obj);
                    if (!obj.id) {
                        obj.id = generateId();
                    };
                    obj.createAt = now;
                    obj.updateAt = now;
                    obj.version = 0;
                } else {
                    console.log('will update entity...' + obj);
                    obj.updateAt = now;
                    obj.version++;
                }
            }
        }
    });
};

var TYPES = ['STRING', 'INTEGER', 'BIGINT', 'TEXT', 'DOUBLE', 'DATEONLY', 'BOOLEAN'];

var exp = {
    defineModel: defineModel,
    sync: () => {
        if (process.env.NODE_ENV !== 'production') {
            sequelize.sync({
                force: true
            });
        } else {
            throw new Error('Cannot sync() when NODE_ENV is set to \'production\'.');
        }
    }
};

for (var type of TYPES) {
    exp[type] = Sequelize[type];
};

exp.ID = ID_TYPE;
exp.generateId = generateId;

module.exports = exp;

//init-db.js
var model = require('./model.js');
model.sync();
//model.js
var fs = require('fs');
var db = require('./db');
var files = fs.readdirSync(__dirname + '/models');
var js_files = files.filter((f) => {
    return f.endsWith('.js');
});
module.exports = {};
for (var f of js_files) {
    console.log(`import model from file ${f}...`);
    var name = f.substring(0, f.length - 3);
    module.exports[name] = require(__dirname + '/models/' + f);
}
module.exports.sync = () => {
    db.sync();
};
//config.js
var defaultConfig = './config-default.js';

var overrideConfig = './config-override.js';

var testConfig = './config-test.js';

var fs = require('fs');

var config = null;

if (process.env.NODE_ENV === 'test') {
    console.log(`load ${testConfig}...`);
    config = require(testConfig);
} else {
    console.log(`load ${defaultConfig}...`);
    config = require(defaultConfig);
    try {
        if (fs.statSync(overrideConfig).isFile()) {
            console.log(`load ${overrideConfig}...`);
            config = Object.assign(config, require(overrideConfig));
            console.log(config);
        }
    } catch (err) {
        console.log(`Cannot load ${overrideConfig}`);
    }
};

module.exports = config;

//config-default.js
var config = {
    dialect: 'mysql',
    database: 'test',
    username: 'root',
    password: '123',
    host: 'localhost',
    port: 3306
};

module.exports = config;
//app.js
var model = require('./model');

var Pet = model.Pet;
var User = model.User;

(async () => {
    var user = await User.create({
        name: 'John',
        gender: false,
        email: 'john-' + Date.now() + '@garfield.pet',
        passwd: 'hahaha'
    });
    console.log('created' + JSON.stringify(user));
    var cat = await Pet.create({
        ownerId: user.id,
        name: 'Garfield',
        gender: false,
        birth: '2007-07-07',
    });
    console.log('created: ' + JSON.stringify(cat));
})();
//Pet.js
var db = require('../db');
module.exports = db.defineModel('pets', {
    ownerId: db.ID,
    name: db.STRING(100),
    gender: db.BOOLEAN,
    birth: db.STRING(10),
})
```

### mocha

mocha是JavaScript的一种单元测试框架，既可以在浏览器环境下运行，也可以在Node.js环境下运行。

* 既可以测试简单的JavaScript函数，又可以测试异步代码，因为异步是JavaScript的特性之一；
* 可以自动运行所有测试，也可以只运行特定的测试；
* 可以支持before、after、beforeEach和afterEach来编写初始化代码。

如果一个模块在运行的时候并不需要，仅仅在开发时才需要，就可以放到devDependencies中。这样，正式打包发布时，devDependencies的包不会被包含进来。

然后使用npm install -D package安装

#### 编写测试
```javascript
// hello-test/
// |
// +- .vscode/
// |  |
// |  +- launch.json <-- VSCode 配置文件
// |
// +- hello.js <-- 待测试js文件
// |
// +- test/ <-- 存放所有test
// ｜ ｜
// |  +- hello-test.js <-- 测试文件
// |
// +- package.json <-- 项目描述文件
// |
// +- node_modules/ <-- npm安装的所有依赖包
//hello.js
module.exports = function (...rest) {
    var sum = 0;
    for (var n of rest) {
        sum += n;
    }
    return sum;
}
//hello-test.js
var assert = require('assert');

var sum = require('../hello');

describe("#helo.js", () => {

    before(function(){
        console.log('before');
    });

    after(function(){
        console.log('after');
    });

    beforeEach(function(){
        console.log('beforeEach');
    });

    afterEach(function(){
        console.log('afterEach');
    });
    it('sum() shoud return 0', () => {
        assert.strictEqual(sum(), 0);
    });
    it('sum(1) should return 1', () => {
        assert.strictEqual(sum(1), 1);
    });

    it('sum(1, 2) should return 3', () => {
        assert.strictEqual(sum(1, 2), 3);
    });

    it('sum(1, 2, 3) should return 6', () => {
        assert.strictEqual(sum(1, 2, 3), 6);
    });
});
```
mocha默认执行test目录下的所有测试,不要去改变默认目录

#### 异步测试
```javascript
// async-test/
// |
// +- .vscode/
// |  |
// |  +- launch.json <-- VSCode 配置文件
// |
// +- hello.js <-- 待测试js文件
// |
// +- data.txt <-- 待测试js文件
// |
// +- test/ <-- 存放所有test
// ｜ ｜
// |  +- await-test.js <-- 测试文件
// |
// +- package.json <-- 项目描述文件
// |
// +- node_modules/ <-- npm安装的所有依赖包

//hello.js
var fs= require('mz/fs');

module.exports=async()=>{
    var expression=await fs.readFile('./data.txt','utf-8');
    var fn = new Function('return '+expression);
    var r = fn();
    console.log(`Calculate:${expression}=${r}`);
    return r;
}
//data.txt
//1 + (2 + 4) * (9 - 2) / 3
//await-test.js

var assert=require('assert');
var hello=require('../hello');

describe('#async hello',()=>{
    describe('#asyncCalculate',()=>{
        it("#async with done",(done)=>{
            (async function(){
                try{
                    var r = await hello();
                    assert.strictEqual(r,15);
                    done();
                }catch(err){
                    done(err);
                }
            })();
        });
        it('#async function', async () => {
            let r = await hello();
            assert.strictEqual(r, 15);
        });

        it('#sync function', () => {
            assert(true);
        });
    });
})
```

#### Http测试
```javascript
// koa-test/
// |
// +- .vscode/
// |  |
// |  +- launch.json <-- VSCode 配置文件
// |
// +- app.js <-- 待测试js文件
// |
// +- start.js <-- 待测试js文件
// |
// +- test/ <-- 存放所有test
// ｜ ｜
// |  +- app-test.js <-- 测试文件
// |
// +- package.json <-- 项目描述文件
// |
// +- node_modules/ <-- npm安装的所有依赖包
//app.js
var Koa = require('koa');

var app = new Koa();

app.use(async (ctx, next) => {
    var start = new Date().getTime();
    await next();

    var ms = new Date().getTime() - start;
    console.log(`${ctx.request.method} ${ctx.request.url}:${ms}ms`);
    ctx.response.set('X-Response-Time', `${ms}ms`);
})

app.use(async (ctx, next) => {
    var name = ctx.request.query.name || 'world';
    ctx.response.type = 'text/html';
    ctx.response.body = `<h1>hello,${name}!</h1>`;
});

module.exports=app;
//app-test.js
var request = require('supertest');
var app = require('../app');
describe('#test koa app', () => {
    var server = app.listen(9900);
    describe('#test server', () => {
        it('#test GET /', async () => {
            var res = await request(server)
                .get('/')
                .expect('Content-Type', /text\/html/)
                .expect(200, '<h1>hello,world!</h1>');
        });

        it("#test GET /path?name=Bob", async () => {
            var res = await request(server)
                .get('/path?name=Bob')
                .expect('Content-Type', /text\/html/)
                .expect(200, '<h1>hello,Bob!</h1>');
        });
    });
});
```

#### 运行测试

* 在当前目录下,执行命令``node_modules\mocha\bin\mocha``
* package.json中修改如下``"scripts": {"test": "mocha"},``,在当前目录下执行``npm test``
* launch.json中配置
```javascript
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Run",
            "type": "node",
            "request": "launch",
            "program": "${workspaceRoot}/hello.js",
            "stopOnEntry": false,
            "args": [],
            "cwd": "${workspaceRoot}",
            "preLaunchTask": null,
            "runtimeExecutable": null,
            "runtimeArgs": [
                "--nolazy"
            ],
            "env": {
                "NODE_ENV": "development"
            },
            "externalConsole": false,
            "sourceMaps": false,
            "outDir": null
        },
        {
            "name": "Test",
            "type": "node",
            "request": "launch",
            "program": "${workspaceRoot}/node_modules/mocha/bin/mocha",
            "stopOnEntry": false,
            "args": [],
            "cwd": "${workspaceRoot}",
            "preLaunchTask": null,
            "runtimeExecutable": null,
            "runtimeArgs": [
                "--nolazy"
            ],
            "env": {
                "NODE_ENV": "test"
            },
            "externalConsole": false,
            "sourceMaps": false,
            "outDir": null
        }
    ]
}
```
注意第一个配置选项``Run``是正常执行一个.js文件，第二个配置选项``Test``我们填入``"program": "${workspaceRoot}/node_modules/mocha/bin/mocha"，``并设置``env为"NODE_ENV": "test"``，这样，就可以在VS Code中打开Debug面板，选择Test，运行，即可在Console面板中看到测试结果：

### webSocket

WebSocket是HTML5新增的协议,WebSocket并不是全新的协议，而是利用了HTTP协议来建立连接,让浏览器和服务器之间可以建立无限制的全双工通信，任何一方都可以主动发消息给对方
首先，WebSocket连接必须由浏览器发起，因为请求协议是一个标准的HTTP请求，格式如下
```
GET ws://localhost:3000/ws/chat HTTP/1.1
Host: localhost
Upgrade: websocket
Connection: Upgrade
Origin: http://localhost:3000
Sec-WebSocket-Key: client-random-string
Sec-WebSocket-Version: 13
```
该请求和普通的HTTP请求有几点不同：
* GET请求的地址不是类似/path/，而是以ws://开头的地址
* 请求头Upgrade: websocket和Connection: Upgrade表示这个连接将要被转换为WebSocket连接；
* Sec-WebSocket-Key是用于标识这个连接，并非用于加密数据；
* Sec-WebSocket-Version指定了WebSocket的协议版本。
随后，服务器如果接受该请求，就会返回如下响应：
```
HTTP/1.1 101 Switching Protocols
Upgrade: websocket
Connection: Upgrade
Sec-WebSocket-Accept: server-random-string
```
该响应代码101表示本次连接的HTTP协议即将被更改，更改后的协议就是Upgrade: websocket指定的WebSocket协议

在Node.js中，使用最广泛的WebSocket模块是ws

#### ws模块

* 开启服务端
```javascript

// 导入WebSocket模块:
var WebSocket= require('ws');
// 引用Server类:
var WebSocketServer = WebSocket.Server;

// 实例化
var wss=new WebSocketServer({
    port:3000
})

wss.on('connection',function(ws){
    console.log(`[SERVER] connection()`);
    ws.on("message",function(message){
        console.log(`[SERVER] Received:${message}`);
        ws.send(`ECHO:${message}`,(err)=>{
            if(err){
                console.log(`[SERVER] error:${err}`);
            }
        });
    });
});
```


* 客户端连接
```javascript
// 导入WebSocket模块:
var WebSocket= require('ws');

var ws = new WebSocket("ws://localhost:3000");
ws.on('open',function(){
    console.log(`[CLIENT] open()`);
    ws.send('Hello!');
});
// 响应收到的消息:
ws.on('message', function (message) {
    console.log(`[CLIENT] Received: ${message}`);
})
```

#### mvc中集成websocket

### REST

REST就是一种设计API的模式。最常用的数据格式是JSON。把网页视为一种客户端，是REST架构可扩展的一个关键。

编写REST API，实际上就是编写处理HTTP请求的async函数，不过，REST请求和普通的HTTP请求有几个特殊的地方：
* REST请求仍然是标准的HTTP请求，但是，除了GET请求外，POST、PUT等请求的body是JSON数据格式，请求的Content-Type为application/json；
* REST响应返回的结果是JSON数据格式，因此，响应的Content-Type也是application/json。

REST API规范
* 例如，商品Product就是一种资源。获取所有Product的URL如下：``GET /api/products``
* 而获取某个指定的Product，例如，id为123的Product，其URL如下：``GET /api/products/123``
* 新建一个Product使用POST请求，JSON数据包含在body中，URL如下：``POST /api/products``
* 更新一个Product使用PUT请求，例如，更新id为123的Product，其URL如下：``PUT /api/products/123``
* 删除一个Product使用DELETE请求，例如，删除id为123的Product，其URL如下：``DELETE /api/products/123``
* 当我们只需要获取部分数据时，可通过参数限制返回的结果集，例如，返回第2页评论，每页10项，按时间排序：``GET /api/products/123/reviews?page=2&size=10&sort=time``

#### koa处理REST



## webpack

本质上，webpack 是一个现代 JavaScript 应用程序的静态模块打包器(module bundler)。当 webpack 处理应用程序时，它会递归地构建一个依赖关系图(dependency graph)，其中包含应用程序需要的每个模块，然后将所有这些模块打包成一个或多个 bundle.

前端自动化构建工具,构建工具就是将源代码转换成可以执行的js、css、html代码.如:
* less 解析less成css
```
lessc demo.less //直接在命令窗口看构建的css
lessc demo.less > demo.css //构建css文件并输出到demo.css
```
* uplify-js 压缩js文件
```
uglifyjs demo.js -o demo.min.js
```
* browserify commonjs规范的模块化,浏览器并不兼容,通过browserify可以构建浏览器支持的js
```
browserify main.js -o bundle.js
```
构建工具主要包括以下几个方面
* 代码转化,如将typescript编译成javascript、将scss编译成css等.
* 文件优化,压缩js、css、html代码,压缩合并图片等.
* 代码分割,提取多个页面的公共代码,提取首屏不需要执行部分代码让其异步加载
* 模块合并,在采用模块化的项目中会有很多个模块和文件,需要通过构建工具将其合并成一个文件
* 自动刷新,监听本地源代码,自动构建、刷新浏览器
* 代码校验,在代码提交到仓库前校验代码是否符合规范,以及单元测试是否通过
* 自动发布,更新代码后,自动构建上线代码发布并传输给发布系统

常用的自动构建工具
* 基于任务的,Grunt、Gulp
* 基于模块的,Browserify、Webpack、rollup.js
* 整合型工具,Yeoman、FIS、jdf、Athena


webpack从4版本开始支持零配置打包,默认会找当前目录下src/index.js文件.默认只能处理js文件,处理其他文件需要加载不同的loader.webpack默认支持commonjs和es6.
* 默认配置,在一个有``src/index.js``目录下执行``webpack``会自动生成``dist/main.js``
* 个性配置,在一个有``demo.js``目录下执行``webpack demo.js -o bundle.js``会自动生成``bundle.js``
* ``npm init``初始化一个项目,会生成一个package.json配置文件,会记录当前项目依赖项.
* ``npm install package -D``本项目下安装,开发环境需要,生产环境不需要
* ``npm install package``本项目下安装,开发和生成环境都需要
* ``npm install package -g``全局安装

### webpack核心概念

* 入口 指示 webpack 应该使用哪个模块，来作为构建其内部依赖图的开始
```javascript
单入口
module.exports={
    entry:'./src/index.js',//入口
    output:{
        path:path.resolve(__dirname,'dist'),//输出目录
        filename:'my-first-webpack.bundle.js',//输出文件名
    },//输出
    mode:'development',//模式
}
```
* 输出 告诉 webpack 在哪里输出它所创建的 bundles，以及如何命名这些文件，默认值为 ./dist
```javascript
多入口 多输出
module.exports={
    entry:{
        index:'./src/index.js',
        app:'./src/app.js'
    },//入口
    output:{
        path:path.resolve(__dirname,'dist'),//输出目录
        filename:'[name].bundle.js',//输出文件名
    },//输出
    mode:'development',//模式
}
```
* loader loader 让 webpack 能够去处理那些非 JavaScript 文件（webpack 自身只理解 JavaScript）
```javascript
loader
module.exports = {
    entry: {
        index: './src/index.js',
        app: './src/app.js'
    }, //入口
    output: {
        path: path.resolve(__dirname, 'dist'), //输出目录
        filename: '[name].bundle.js', //输出文件名
    }, //输出
    module: {
        //需要在入口文件中引入less文件才可以解析
        rules: [{
            test: /\.less$/,
            use: ['style-loader', 'css-loader', 'less-loader']//从后往前解析
        }] 
    },
    mode: 'development', //模式
}
```
* 插件 loader 被用于转换某些类型的模块，而插件则可以用于执行范围更广的任务
```javascript
var HtmlWebpackPlugin = require('html-webpack-plugin');
//插件
module.exports = {
    entry: {
        index: './src/index.js',
        app: './src/app.js'
    }, //入口
    output: {
        path: path.resolve(__dirname, 'dist'), //输出目录
        filename: '[name].bundle.js', //输出文件名
    }, //输出
    module: {
        //需要在入口文件中引入less文件才可以解析
        rules: [{
            test: /\.less$/,
            use: ['style-loader', 'css-loader', 'less-loader']//从后往前解析
        }] 
    },
    plugins:[
        new HtmlWebpackPlugin()
    ],
    mode: 'development', //模式
}
```

### 常用插件及loader

* webpack-deep-scope-plugin
```javascript
var webpackDeepScopeAnalysisPlugin = require('webpack-deep-scope-plugin').default;
module.exports={
    plugins:[
        new webpackDeepScopeAnalysisPlugin(),
    ]
}
```
webpack构建生产环境对js的压缩、抖动(过滤一些无用代码),但是对于作用域级别的引用,无法做到很好的抖动.该插件可以弥补这一点,更好的实现抖动

* mini-css-extract-plugin
```javascript
const MiniCssExtractPlugin = require('mini-css-extract-plugin');
module.exports={
    module:{
        rules:[
            {
                test:/\.css$/,
                use:[MiniCssExtractPlugin.loader,'css-loader']
            }
        ]
    },
    plugins:[
        new MiniCssExtractPlugin({
            // Options similar to the same options in webpackOptions.output
            // all options are optional
            filename: '[name].css',
            //chunkFilename: '[id].css',
            ignoreOrder: false, // Enable to remove warnings about conflicting order
          }),
    ],
    mode:'production'
}
```
此插件将 CSS 提取到单独的文件中,

* purifycss-webpack
```javascript
const glob = require('glob-all')
const PurifyCSSPlugin = require('purifycss-webpack');
const MiniCssExtractPlugin = require('mini-css-extract-plugin');
module.exports={
    module:{
        rules:[
            {
                test:/\.css$/,
                use:[MiniCssExtractPlugin.loader,'css-loader']
            }
        ]
    },
    plugins:[
        new webpackDeepScopeAnalysisPlugin(),
        new MiniCssExtractPlugin({
            // Options similar to the same options in webpackOptions.output
            // all options are optional
            filename: '[name].css',
            //chunkFilename: '[id].css',
            ignoreOrder: false, // Enable to remove warnings about conflicting order
          }),
        new PurifyCSSPlugin({
            // Give paths to parse for rules. These should be absolute!
            // paths: glob.sync(path.join(__dirname, './*.html'),
            paths: glob.sync(
                [
                    path.join(__dirname, './*.html'),
                    path.join(__dirname,'./src/*.js')
                ])
          })
      
    ],
    mode:'production'
}
```
此插件使用PurifyCSS从CSS中删除未使用的选择器


### 出入口、loader、插件


1. 默认

```css
/* 默认入口找当前目录下的src文件夹index.js进行打包 */
webpack

/* 默认出口当前目录下的dist文件夹main.js*/
```

2. 指定打包文件

```cmd
webpack demo.js -o bundle.js
```

3. webpack.config.js

遵循common.js

```javascript
var HtmlWebpackPlugin=require('html-webpack-plugin');
//插件
var path=require('path');
module.exports={
    // entry:'./src/index.js',
    //入口
    // output:{
    //     path:path.resolve(__dirname,'dist')
    //     filename:'my-first-webpack.bundle.js'
    // },
    //出口
    entry:{
        index:'./src/index.js',
        app:'./src/app.js'
    },
     output:{
        path:path.r esolve(__dirname,'dist')
        filename:'[name].bundle.js'
    },
    mode:'devlopment'
    //模式

    module:{
        rules:[
            { test:/\.less$/,use:['style-loader','css-loader','less-loader'] }
            //从后往前解析less-loader->css-loader->style-loader
        ]
    },
    //loader被用于转某些类型的模块

    plugins:[
        new HtmlWebpackPlugin({template:'./src/index.html'})
    ]
    //插件
}
```

### js tree shaking

打包的时候删除一些无用的代码,webpack本身对作用域的代码无法检测,需要借助插件(webpack-deep-scope-plugin)来更好的shaking

### css tree shaking

webpack自身不支持抖动css

打包的时候删除一些没有引用的样式代码

mini-css-extract-plugi 单独抽离css文件

purfycss-webpack 打包抖掉无用的css文件

css抖动放在js前

注释会被匹配掉,不会抖掉



### postcss

1. 把css解析成js,解析成语法树
2. 调用插件操作语法树(autoprefixer(加前缀)、cssnano(压缩)、)

### htmlwebpackplugin

自动生成html文件并引入css、js文件

### 提取公共js代码

### 图片处理

url-loader 处理关于图片打包

### 开启本地服务器

web-dev-server

webpack -w  不开启服务监听本地文件变化

### 热更新

HotModuleReplacementPlugin();插件

## gulp

gulp强调的是前端开发的工作流程，我们可以通过配置一系列的task，定义task处理的事务（例如文件压缩合并、雪碧图、启动server、版本控制等），然后定义执行顺序，来让gulp执行这些task，从而构建项目的整个前端开发流程。

简单说就一个Task Runner

```javascript
var {
    watch,
    series,
    task,
    dest,
    src
} = require('gulp');

//压缩html插件
var htmlclean = require('gulp-htmlclean');
//压缩图片狗比玩意里面的默认插件,非常容易安装失败,多安装即便,再默认源和淘宝源之间尝试切换
var imageMin = require('gulp-imagemin');
//压缩js
var uglify = require('gulp-uglify');
//去掉js中的调试语句
const stripDebug = require('gulp-strip-debug');
//将less转换成css
var less = require('gulp-less');
//css压缩
let cleanCSS = require('gulp-clean-css');
//css添加前缀
var postcss = require('gulp-postcss');
var autoprefixer = require('autoprefixer');

//开启服务器
var connect = require("gulp-connect");

var folder = {
    src: "src/",
    dist: "dist/"
}
var devMode = process.env.NODE_ENV == "development";
//export NODE_ENV=development 设置环境变量
task("html", function (cb) {
    //直接输出
    // src(folder.src + "html/*")
    //     .pipe(dest(folder.dist + "html/"))

    //压缩输出
    src(folder.src + "html/*")
        .pipe(connect.reload())
        .pipe(htmlclean())
        .pipe(dest(folder.dist + "html/"))
    cb();
});

task("css", function (cb) {
    src(folder.src + "css/*")
        .pipe(connect.reload()) //自动刷新的
        .pipe(cleanCSS())
        .pipe(dest(folder.dist + "css/"))
    cb();
});

task("less", function (cb) {
    src(folder.src + "less/*")
        .pipe(less())
        .pipe(postcss([autoprefixer()]))
        .pipe(cleanCSS())
        .pipe(dest(folder.dist + "less/"))
    cb();
});

task("js", function (cb) {
    var page = src(folder.src + "js/*")
        .pipe(stripDebug())
        if(!devMode){//判断压缩
            page.pipe(uglify())
        }
        page.pipe(dest(folder.dist + "js/"))
    cb();
});

task("image", function (cb) {
    src(folder.src + "images/*")
        .pipe(imageMin())
        .pipe(dest(folder.dist + "images/"))
    cb();
});

task("server", function (cb) {
    connect.server({
        port: 8888,
        livereload: true //开启文件变化
    });
    cb();
});

//监听文件
task("watch", function (cb) {
    watch(folder.src + "html/*", series("html"));
    watch(folder.src + "css/*", series("css"));
    cb();
});

exports.default = series("html", "js", "css", "less", "image", "server", "watch");
```

