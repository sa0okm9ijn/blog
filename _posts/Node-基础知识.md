---
title: Node-基础知识
date: 2019-12-10 15:01:37
tags:
---

# less

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

# node.js

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


## 模块化

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


### AMD
### CMD
### Es6





为啥我们需要一个包管理工具呢？因为我们在Node.js上开发时，会用到很多别人写的JavaScript代码。如果我们要使用别人写的某个包，每次都根据名称搜索一下官方网站，下载代码，解压，再使用，非常繁琐。于是一个集中管理的工具应运而生：大家都把自己开发的模块打包后放到npm官网上，如果要使用，直接通过npm安装就可以直接用，不用管代码存在哪，应该从哪下载。

更重要的是，如果我们要使用模块A，而模块A又依赖于模块B，模块B又依赖于模块X和模块Y，npm可以根据依赖关系，把所有依赖的包都下载下来并管理起来。否则，靠我们自己手动管理，肯定既麻烦又容易出错。

讲了这么多，npm究竟在哪？

其实npm已经在Node.js安装的时候顺带装好了。我们在命令提示符或者终端输入npm -v，应该看到类似的输出：

```
npm -v
6.9.0
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

url2-koa/
|
+- controllers/
|  |
|  +- hello.js <-- 处理login相关URL
|  |
|  +- index.js <-- 处理用户管理相关URL
|
+- app.js <-- 使用koa的js
|
+- controller.js <-- 自动处理url函数js
|
+- package.json <-- 项目描述文件
|
+- node_modules/ <-- npm安装的所有依赖包


* 重构
```javascript
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








### webpack

前端自动化构建工具.

我们现在对node有了大概的了解,通俗的说node就是一种运行与服务器端的环境,他的语言是javascript,类似.Net平台它的语言是c#.其次,Node提供大量工具库，使得JavaScript语言与操作系统互动（比如读写文件、新建子进程），在这个意义上，Node又是JavaScript的工具库。

webpack无配置打包


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