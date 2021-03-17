---
title: JavaScript-React基础知识
date: 2020-03-31 21:23:02
tags: 
- React 
categories: JavaScript 
description: 
---

# React概述

> 官网：https://react.docschina.org/

## 什么是React？

React是由**Facebook**研发的、用于**解决UI复杂度**的开源**JavaScript库**，目前由React联合社区维护。

> 它不是框架，只是为了解决UI复杂度而诞生的一个库

## React的特点

- 轻量：React的开发版所有源码（包含注释）仅3000多行
- 原生：所有的React的代码都是用原生JS书写而成的，不依赖其他任何库
- 易扩展：React对代码的封装程度较低，也没有过多的使用魔法，所以React中的很多功能都可以扩展。
- 不依赖宿主环境：React只依赖原生JS语言，不依赖任何其他东西，包括运行环境。因此，它可以被轻松的移植到浏览器、桌面应用、移动端。
- 渐近式：React并非框架，对整个工程没有强制约束力。这对与那些已存在的工程，可以逐步的将其改造为React，而不需要全盘重写。
- 单向数据流：所有的数据自顶而下的流动
- 用JS代码声明界面
- 组件化

## 对比Vue

|   对比项   |  Vue  | React |
| :--------: | :---: | :---: |
| 全球使用量 |       |   ✔   |
| 国内使用量 |   ✔   |       |
|    性能    |   ✔   |   ✔   |
|   易上手   |   ✔   |       |
|   灵活度   |       |   ✔   |
|  大型企业  |       |   ✔   |
| 中小型企业 |   ✔   |       |
|    生态    |       |   ✔   |

## 学习路径

整体原则：熟悉API --> 深入理解原理
1. React
   1. 基础：掌握React的基本使用方法，有能力制作各种组件，并理解其基本运作原理
   2. 进阶：掌握React中的一些黑科技，提高代码质量
2. React-Router：相当于vue-router
3. Redux：相当于Vuex
   1. Redux本身
   2. 各种中间件
4. 第三方脚手架：umi
5. UI库：Ant Design，相当于Vue的Element-UI 或 IView
6. 源码部分
   1. React源码分析
   2. Redux源码分析

## 关于课程

- demo关键字：课程名称前有**demo**字样的，为一个小练习，需要同学听完讲解后自行独立完成
- 扩展关键字：课程名称前有**扩展**字样的，为选修内容，没有掌握不会影响后面的学习
- 关于源代码：本门课所有源代码均使用git管理，每节课的代码为独立分支，但某些文件夹和文件不属于源代码管理范畴。
- 关于npm：本门课所有的第三方库安装，均使用yarn

# HelloWorld

直接在页面上使用React,引用下面的JS

```html
<!-- React的核心库，与宿主环境无关 -->
<script crossorigin src="https://unpkg.com/react@16/umd/react.development.js"></script>
<!-- 依赖核心库，将核心的功能与页面结合 -->
<script crossorigin src="https://unpkg.com/react-dom@16/umd/react-dom.development.js"></script>
<!-- 编译JSX -->
<script src="https://unpkg.com/babel-standalone@6/babel.min.js"></script>
```

## React.createElement

创建一个React元素，称作虚拟DOM，本质上是一个对象
1. 参数1：元素类型，如果是字符串，一个普通的HTML元素
2. 参数2：元素的属性，一个对象
3. 后续参数：元素的子节点

```js
<script>
   var span = React.createElement('span', {}, '一个span元素');
   var h1 = React.createElement('h1', { title: '第一个React元素' }, 'hello', 'world', span);
   ReactDOM.render(h1, document.getElementById('root'));
</script>
```

## JSX
JS的扩展语法，需要使用babel进行转义。在浏览器中使用需要标准type让浏览器不要解析
```js
<script type="text/babel">

   var span = <span>一个元素</span>
   var h1 = <h1 title='第一个React元素'>Hello world </h1>
   ReactDOM.render(h1, document.getElementById('root'))
</script>
```

# 使用脚手架搭建工程

官方：create-react-app
第三方：next.js、umijs

凡是使用JSX的文件，必须导入React

我们使用官方脚手架搭建工程,搭建完成之后如下目录
├── public
├── ├── favicon.ico
├── ├── index.html
├── src
├── ├── index.js

上面的目录是经过精简的,删掉多余的文件,修改index.html,删除多余内容

``index.js``
```js
ReactDOM.render(
  <h1>hello world  <span>span元素</span></h1>
  ,document.getElementById('root')
);
```


# 开发环境搭建

## VSCode配置

emmet配置：

```json
"emmet.includeLanguages": {
   "javascript":"javascriptreact"
}
```

## VSCode插件安装

- ESLint：代码风格检查
- ES7 React/Redux/GraphQL/React-Native snippets：快速代码编写

## Chrome插件安装

React Developer Tools

# JSX

## 什么是JSX

- Facebook起草的JS扩展语法
- 本质是一个JS对象，会被babel编译，最终会被转换为React.createElement
- 每个JSX表达式，有且仅有一个根节点
  - React.Fragment
  ```js
  //代表一个空的根节点,可以简写未<></>
  const h1 = (
   <React.Fragment>
   <h1>Hello world <span>span1元素</span></h1>
   </React.Fragment>
   )
  ```
- 每个JSX元素必须结束（XML规范）

## 在JSX中嵌入表达式

- 在JSX中使用注释
- 将表达式作为内容的一部分
  - null、undefined、false不会显示
  - 普通对象，不可以作为子元素
  - 可以放置React元素对象
  ```js
   // const obj = {
   //   a:1,
   //   b:2
   // }
   const obj = <span>这是一个span元素</span>
   const a =123,b =432;
   const arr = [2,null,false,undefined,3]

   const numbers=new Array(30);
   numbers.fill(0);
   var lis = numbers.map((item,i)=>(<li key={i}>{i}</li>))

   const div = (
   <div>
      {a}*{b}={a*b}
      <p>
         {/* 以下不会产生任何输出 */}
         {null}
         {undefined}
         {false}
      </p>
      <p>
         {/*普通对象无法放置,React元素对象没问题*/}
         {obj}
      </p>
      <p>
         {arr}
      </p>
      <p>
         {numbers}
      </p>
      <p>
         {lis}
      </p>
   </div>
   )

   ReactDOM.render(div,
   document.getElementById('root')
   );
  ```
- 将表达式作为元素属性
- 属性使用小驼峰命名法
```js
const url = "https://ss1.bdstatic.com/70cFvXSh_Q1YnxGkpoWK1HF6hhy/it/u=2962719555,3613138778&fm=27&gp=0.jpg";
const cls = "image";
const div = (
  <div>
    <img src={url} className={cls} style={{marginLeft:'50px',width:'200px'}} alt=""/>
  </div>
)

ReactDOM.render(div,
  document.getElementById('root')
);
```
- 防止注入攻击
  - 自动编码
  - dangerouslySetInnerHTML
```js
const content = "<h1>afasfasfd</h1><p>阿斯顿法定发送</p>";

const div = (
  <div dangerouslySetInnerHTML={{
    __html:content
  }}>
  </div>
)

ReactDOM.render(div,
  document.getElementById('root')
);
```
## 元素的不可变性

- 虽然JSX元素是一个对象，但是该对象中的所有属性不可更改
- 如果确实需要更改元素的属性，需要重新创建JSX元素

```js
let num = 0;
 
setInterval(() => {
    num++;
    const div = (
      <div title="asdfadf">
          {num}
      </div>
    );
    ReactDOM.render(div,
      document.getElementById('root')
    );
}, 1000);
```


# 组件和组件属性

组件：包含内容、样式和功能的UI单元

## 创建一个组件

**特别注意：组件的名称首字母必须大写**

1. 函数组件
   
返回一个React元素

```js
import React from 'react'
export default function MyFuncComp(props){
    return <h1>函数组件,目前的数字:{props.number}</h1>
}
```

2. 类组件

必须继承React.Component

必须提供render函数，用于渲染组件

```js
import React from 'react'


export default class MyClassComp extends React.Component {
    // constructor(props) {
    //     super(props);
    //     console.log(props, this.props, props === this.props);
    // }
    render() {
        if(this.props.obj){
            return <>
                <p>姓名:{this.props.obj.name}</p>
                <p>年龄:{this.props.obj.age}</p>
            </>
        }else if(this.props.ui){
            return <>
                <div>
                    <h1>下面是传入的内容</h1>
                    {this.props.ui}
                </div>
            </>
        }
    return <h1>类组件的内容,数字:{this.props.number}</h1>
    }
}
```

## 组件的属性

1. 对于函数组件，属性会作为一个对象的属性，传递给函数的参数
2. 对于类组件，属性会作为一个对象的属性，传递给构造函数的参数

注意：组件的属性，应该使用小驼峰命名法

**组件无法改变自身的属性**。

之前学习的React元素，本质上，就是一个组件（内置组件）

```js

import MyFuncComp from './MyFuncComp'
import MyClassComp from './MyClassComp'

const comp = <MyFuncComp number={3}></MyFuncComp>

console.log(comp);

const div =<div title="ASDA"></div>
/console.log(div);
```

React中的哲学：数据属于谁，谁才有权力改动

**React中的数据，自顶而下流动**


# 组件状态

组件状态：组件可以自行维护的数据

组件状态仅在类组件中有效

状态（state），本质上是类组件的一个属性，是一个对象

**状态初始化**

**状态的变化**

不能直接改变状态：因为React无法监控到状态发生了变化

必须使用this.setState({})改变状态

一旦调用了this.setState，会导致当前组件重新渲染
```js
export default class Tick extends Component {
    //初始化状态,JS Next语法 目前处于实验阶段  //初始化可以写在构造函数中
    state={
        left:this.props.number,
        n:123
    }
    constructor(props){
        super(props);

        this.timer = setInterval(() => {
            this.setState({
                left:this.state.left-1
            });
            if(this.state.left ===0){
                clearInterval(this.timer);
            }
        }, 1000);
    }
    render() {
        return (
            <div>
                <h1>倒计时剩余时间:{this.state.left}</h1>
            </div>
        )
    }
}

```

**组件中的数据**

1. props：该数据是由组件的使用者传递的数据，所有权不属于组件自身，因此组件无法改变该数组
2. state：该数组是由组件自身创建的，所有权属于组件自身，因此组件有权改变该数据

# 事件

在React中，组件的事件，本质上就是一个属性

按照之前React对组件的约定，由于事件本质上是一个属性，因此也需要使用小驼峰命名法


**如果没有特殊处理，在事件处理函数中，this指向undefined**

1. 使用bind函数，绑定this
2. 使用箭头函数

```js
export default class TickControl extends Component {
    state={
        isOver:false
    }
    //constructor(props){
    //     super(props);
    //     this.handleClick = this.handleClick.bind(this);
    //     this.handleOver = this.handleOver.bind(this);
    // }
    handleClick= ()=>{
        console.log(this)
        console.log("点击了")
    }
    handleOver= ()=>{
        console.log(this);
        this.setState({
            isOver: true
        })
    }
    render() {
        let status="正在倒计时";
        if(this.state.isOver){
            status="倒计时完成"
        }
        return (
            <div>
                <Tick number={10} onClick={this.handleClick} onOver={this.handleOver}></Tick>
                <h2>
                    {status}
                </h2>
            </div>
        )
    }
}

```


# 深入认识setState

setState，它对状态的改变，**可能**是异步的

> 如果改变状态的代码处于某个HTML元素的事件中，则其是异步的，否则是同步

```js
export default class Comp extends Component {
    state={
        n:0
    }
    handleClick = ()=>{
        this.setState({
            n:this.state.n+1
        })
        console.log(this.state.n);//还没有重新渲染，说明目前状态仍然没有改变
    }
    render() {
        console.log('render');
        return (
            <div>
                    <h1>
                        {this.state.n}
                    </h1>
                    <p>
                        <button onClick={this.handleClick}>+</button>
                    </p>
            </div>
        )
    }
}
```

如果遇到某个事件中，需要同步调用多次，需要使用函数的方式得到最新状态

最佳实践：

1. 把所有的setState当作是异步的
2. 永远不要信任setState调用之后的状态
3. 如果要使用改变之后的状态，需要使用回调函数（setState的第二个参数）
```js
export default class Comp extends Component {
    state={
        n:0
    }
    handleClick = ()=>{
        this.setState({
            n:this.state.n+1
        },()=>{
            console.log(this.state.n);//还没有重新渲染，说明目前状态仍然没有改变
        })
        
    }
    render() {
        console.log('render');
        return (
            <div>
                    <h1>
                        {this.state.n}
                    </h1>
                    <p>
                        <button onClick={this.handleClick}>+</button>
                    </p>
            </div>
        )
    }
}
```
4. 如果新的状态要根据之前的状态进行运算，使用函数的方式改变状态（setState的第一个函数）
```js
this.setState(cur=>{
   return {
      n:cur.n+1
   }
},()=>{
   //所有状态全部更新完成，并且重新渲染后执行
   console.log("state更新完成", this.state.n);
})
```
React会对异步的setState进行优化，将多次setState进行合并（将多次状态改变完成后，再统一对state进行改变，然后触发render）

1. 同步调用不会优化
```js
export default class Comp extends Component {
    state={
        n:0
    }
    constructor(props){
        super(props);
        setInterval(() => {
            this.setState({
                n:this.state.n+1
            })
            this.setState({
                n:this.state.n+1
            })
            this.setState({
                n:this.state.n+1
            })
        }, 1000);
    }
    render() {
        console.log('render');
        return (
            <div>
                    <h1>
                        {this.state.n}
                    </h1>
                    <p>
                        <button>+</button>
                    </p>
            </div>
        )
    }
}
```

2. 异步调用会优化
```js
export default class Comp extends Component {
    state={
        n:0
    }
    handleClick = ()=>{
       this.setState(cur=>{
           return {
               n:cur.n+1
           }
       },()=>{
           //所有状态全部更新完成，并且重新渲染后执行
           console.log("state更新完成", this.state.n);
       })
       this.setState(cur => ({
        n: cur.n + 1
        }));

        this.setState(cur => ({
            n: cur.n + 1
        }));
    }
    render() {
        console.log('render');
        return (
            <div>
                    <h1>
                        {this.state.n}
                    </h1>
                    <p>
                        <button onClick={this.handleClick}>+</button>
                    </p>
            </div>
        )
    }
}
```

# 生命周期

生命周期：组件从诞生到销毁会经历一系列的过程，该过程就叫做生命周期。React在组件的生命周期中提供了一系列的钩子函数（类似于事件），可以让开发者在函数中注入代码，这些代码会在适当的时候运行。

**生命周期仅存在于类组件中，函数组件每次调用都是重新运行函数，旧的组件即刻被销毁**

## 旧版生命周期

React < 16.0.0
![](/images/旧版生命周期.png)
1. constructor
   1. 同一个组件对象只会创建一次
   2. 不能在第一次挂载到页面之前，调用setState，为了避免问题，构造函数中严禁使用setState
2. componentWillMount
   1. 正常情况下，和构造函数一样，它只会运行一次
   2. 可以使用setState，但是为了避免bug，不允许使用，因为在某些特殊情况下，该函数可能被调用多次
3. **render**
   1. 返回一个虚拟DOM，会被挂载到虚拟DOM树中，最终渲染到页面的真实DOM中
   2. render可能不只运行一次，只要需要重新渲染，就会重新运行
   3. 严禁使用setState，因为可能会导致无限递归渲染
4. **componentDidMount**
   1. 只会执行一次
   2. 可以使用setState
   3. 通常情况下，会将网络请求、启动计时器等一开始需要的操作，书写到该函数中
5. 组件进入活跃状态
6. componentWillReceiveProps
   1. 即将接收新的属性值
   2. 参数为新的属性对象
   3. 该函数可能会导致一些bug，所以不推荐使用
7. **shouldComponentUpdate**
   1. 指示React是否要重新渲染该组件，通过返回true和false来指定
   2. 默认情况下，会直接返回true
8. componentWillUpdate
   1. 组件即将被重新渲染
9. componentDidUpdate
   1.  往往在该函数中使用dom操作，改变元素
10. **componentWillUnmount**
    1.  通常在该函数中销毁一些组件依赖的资源，比如计时器

```js
export default class OldLifeCycle extends Component {
    constructor(props){
        super(props);
        this.state={
            n:0
        }
        console.log('constructor',"一个新的组件诞生了");
    }
    componentWillMount(){
        console.log("componentWillMount", "组件即将被挂载");
    }
    render() {
        console.log('render',"渲染,返回的React元素会被挂载到虚拟DOM树中");
        return (
            <div>
                <h1>旧版声明周期</h1>
                <h2>属性n:{this.props.n}</h2>
                <h2>状态n:{this.state.n}</h2>
                <button onClick={()=>{
                    this.setState({
                        n:this.state.n+1
                    })
                }}>状态n+1</button>
            </div>
        )
    }
    componentDidMount() {
        console.log("componentDidMount", "挂载完成");
    }

    componentWillReceiveProps(nextProps) {
        console.log("componentWillReceiveProps", "接收到新的属性值", this.props, nextProps);
    }

    shouldComponentUpdate(nextProps, nextState) {
        console.log("shouldComponentUpdate", "是否应该重新渲染", this.props, nextProps, this.state, nextState)
        if (this.props.n === nextProps.n && this.state.n === nextState.n) {
            return false;
        }
        return true;
    }

    componentWillUpdate(nextProps, nextState) {
        console.log("componentWillUpdate", "组件即将被重新渲染");
    }

    componentDidUpdate(prevProps, prevState) {
        console.log("componentDidUpdate", "组件已完成重新渲染", prevProps, prevState);
    }

    componentWillUnmount() {
        console.log("componentWillUnmount", "组件被销毁")
    }
    
}

```

## 新版生命周期

![](新版生命周期 .jpg)

React >= 16.0.0


React官方认为，某个数据的来源必须是单一的

```js

export default class Test extends Component {
    state={
        n:this.props.n
    }
    componentWillReceiveProps(nextProps){
        this.setState({
            n:nextProps.n
        })
    }
    render() {
        return (
            <div>
                <h1>数字:{this.state.n}</h1>
                <button onClick={()=>{
                    this.setState({
                        n:this.state.n+1
                    })
                }}>+1</button>
            </div>
        )
    }
}
```

由于``componentWillReceiveProps``容易导致数据的来源不一致等一些其他bug新版生命周期函数中去掉了.

1. getDerivedStateFromProps
   1. 通过参数可以获取新的属性和状态
   2. 该函数是静态的
   3. 该函数的返回值会覆盖掉组件状态
   4. 该函数几乎是没有什么用
2. getSnapshotBeforeUpdate
   1. 真实的DOM构建完成，但还未实际渲染到页面中。
   2. 在该函数中，通常用于实现一些附加的dom操作
   3. 该函数的返回值，会作为componentDidUpdate的第三个参数


```js
export default class NewLifeCycle extends Component {
    state={
        n:this.props.n
    }
    // static getDerivedStateFromProps(props, state) {
    //     console.log(props)
    //     console.log("getDerivedStateFromProps");
    //     // return null;//不改变当前状态
    //     return { //用新的对象替换掉之前的状态 //返回的是状态对象
    //         n: props.n
    //     }
    // }
    getSnapshotBeforeUpdate = (prevProps, prevState) => {
        console.log("getSnapshotBeforeUpdate");
        return 132;
    }
    componentDidUpdate(prevProps, prevState, snap) {
        console.log("componentDidUpdate", snap);
    }
    render() {
        return (
            <div>
                {this.props.n}
                <h1>{this.state.n}</h1>
                <p>
                    <button onClick={()=>{
                        this.setState({
                            n:this.state.n+1
                        })
                    }}>+1</button>
                </p>
            </div>
        )
    }
}
```


# 传递元素内容

内置组件：div、h1、p

```html
<div>
asdfafasfafasdfasdf
</div>
```


如果给自定义组件传递元素内容，则React会将元素内容作为children属性传递过去。

```js
export default function Comp(props) {
    console.log(props)
    return (
        <div className="comp">
            <h1>组件自身内容</h1>
            {props.children || <h1>默认值</h1>}
            {props.content1}
        </div>
    )
}
```

# 表单

受控组件和非受控组件

受控组件：组件的使用者，有能力完全控制该组件的行为和内容。通常情况下，受控组件往往没有自身的状态，其内容完全收到属性的控制。

非受控组件：组件的使用者，没有能力控制该组件的行为和内容，组件的行为和内容完全自行控制。

**表单组件，默认情况下是非受控组件，一旦设置了表单组件的value属性，则其变为受控组件(单选和多选框需要设置checked)**

```js
export default class App extends Component {
    state={
        val:'123',
        loves:['足球','篮球','音乐','其他'],
        chooseLoves:['篮球','音乐'],
        selVal:'beijing'
    }
    render() {
        const checkboxes=this.state.loves.map(it=>(
            <label key={it}>
                <input type="checkbox" checked={this.state.chooseLoves.includes(it)}
                       onChange={e=>{
                           if(e.target.checked){
                               this.setState({
                                   chooseLoves:[...this.state.chooseLoves,it]
                               })
                           }else{
                               this.setState({
                                   chooseLoves:this.state.chooseLoves.filter(l=>l!=it)
                               })
                           }
                       }}
                />
                {it}
            </label>
        ))
        return (
            <div>
                {/*默认情况下,它是一个非受控组件 */}
                {/* {<input type="text" ></input>} */}

                <input type="text" value={this.state.val} onChange={e=>{
                    this.setState({
                        val:e.target.value
                    })
                }}/>
                <button onClick={()=>{
                    console.log(this.state.val)
                }}>获取文本框的值</button>
                <NumberInput></NumberInput>
                {checkboxes}
                <select value={this.state.selVal} onChange={e=>{
                    this.setState({
                        selVal:e.target.value
                    })
                }}>
                     <option value="beijing">北京</option>
                    <option value="shanghai">上海</option>
                    <option value="shenzheng">深证</option>
                </select>
            </div>
        )
    }
}
```


# 属性默认值 和 类型检查


## 属性默认值

通过一个静态属性```defaultProps```告知react属性默认值

## 属性类型检查

使用库：```prop-types```

对组件使用静态属性```propTypes```告知react如何检查属性

```js

PropTypes.any：//任意类型
PropTypes.array：//数组类型
PropTypes.bool：//布尔类型
PropTypes.func：//函数类型
PropTypes.number：//数字类型
PropTypes.object：//对象类型
PropTypes.string：//字符串类型
PropTypes.symbol：//符号类型

PropTypes.node：//任何可以被渲染的内容，字符串、数字、React元素
PropTypes.element：//react元素
PropTypes.elementType：//react元素类型
PropTypes.instanceOf(构造函数)：//必须是指定构造函数的实例
PropTypes.oneOf([xxx, xxx])：//枚举
PropTypes.oneOfType([xxx, xxx]);  //属性类型必须是数组中的其中一个
PropTypes.arrayOf(PropTypes.XXX)：//必须是某一类型组成的数组
PropTypes.objectOf(PropTypes.XXX)：//对象由某一类型的值组成
PropTypes.shape(对象): //属性必须是对象，并且满足指定的对象要求
PropTypes.exact({...})：//对象必须精确匹配传递的数据

//自定义属性检查，如果有错误，返回错误对象即可
属性: function(props, propName, componentName) {
   //...
}
```

# HOC 高阶组件
HOF：Higher-Order Function, 高阶函数，以函数作为参数，并返回一个函数
HOC: Higher-Order Component, 高阶组件，以组件作为参数，并返回一个组件


通常，可以利用HOC实现横切关注点。

> 举例：20个组件，每个组件在创建组件和销毁组件时，需要作日志记录
> 20个组件，它们需要显示一些内容，得到的数据结构完全一致

**注意**

1. 不要在render中使用高阶组件,提前声明好,提高在setState的时候不停的创建和销毁组件
2. 不要在高阶组件内部更改传入的组件.

# ref

reference: 引用

场景：希望直接使用dom元素中的某个方法，或者希望直接使用自定义组件中的某个方法

1. ref作用于内置的html组件，得到的将是真实的dom对象
2. ref作用于类组件，得到的将是类的实例
3. ref不能作用于函数组件

ref不再推荐使用字符串赋值，字符串赋值的方式将来可能会被移出

目前，ref推荐使用对象或者是函数

**对象**

通过 React.createRef 函数创建

**函数**

函数的调用时间：

1. componentDidMount的时候会调用该函数
   1. 在componentDidMount事件中可以使用ref
2. 如果ref的值发生了变动（旧的函数被新的函数替代），分别调用旧的函数以及新的函数，时间点出现在componentDidUpdate之前(函数没有写在外面的情况下)
   1. 旧的函数被调用时，传递null
   2. 新的函数被调用时，传递对象
3. 如果ref所在的组件被卸载，会调用函数

**谨慎使用ref**

能够使用属性和状态进行控制，就不要使用ref。

1. 调用真实的DOM对象中的方法
2. 某个时候需要调用类组件的方法

# Ref转发

ref的指向并不是引用他本身,而是指向它内部的东西.

forwardRef

forwardRef方法：

1. 参数，传递的是函数组件，不能是类组件，并且，函数组件需要有第二个参数来得到ref
2. 返回值，返回一个新的组件

主要是在用高阶组件时侯,想获取高阶组件包装的组件的引用,用Ref转发

# Context

有時候我們希望可以在子組件得到父組件中的状态数据,如果这个子组件层次足够深,我们需要借助属性达到获取的目的,如下

![](属性传递.png)

上下文：Context，表示做某一些事情的环境

React中的上下文特点：

1. 当某个组件创建了上下文后，上下文中的数据，会被所有后代组件共享
2. 如果某个组件依赖了上下文，会导致该组件不再纯粹（外部数据仅来源于属性props）
3. 一般情况下，用于第三方组件（通用组件）

## 旧的API

![](旧版上下文.png)

**创建上下文**

只有类组件才可以创建上下文

1. 给类组件书写静态属性 childContextTypes，使用该属性对上下文中的数据类型进行约束
2. 添加实例方法 getChildContext，该方法返回的对象，即为上下文中的数据，该数据必须满足类型约束，该方法会在每次render之后运行。

**使用上下文中的数据**

要求：如果要使用上下文中的数据，组件必须有一个静态属性 contextTypes，该属性描述了需要获取的上下文中的数据类型

1. 可以在组件的构造函数中，通过第二个参数，获取上下文数据
2. **从组件的context属性中获取**
3. 在函数组件中，通过第二个参数，获取上下文数据
4. 组件中有多个上下文，获取数据就近原则获取.

**上下文的数据变化**

上下文中的数据不可以直接变化，最终都是通过状态改变

在上下文中加入一个处理函数，可以用于后代组件更改上下文的数据

## 新的API
![](新版上下文.png)

旧版API存在严重的效率问题，并且容易导致滥用

**创建上下文**

上下文是一个独立于组件的对象，该对象通过React.createContext(默认值)创建

返回的是一个包含两个属性的对象

1. Provider属性：生产者。一个组件，该组件会创建一个上下文，该组件有一个value属性，通过该属性，可以为其数据赋值
   1. 同一个Provider，不要用到多个组件中，如果需要在其他组件中使用该数据，应该考虑将数据提升到更高的层次
2. Consumer属性：后续讲解

**使用上下文中的数据**

1. 在类组件中，直接使用this.context获取上下文数据
   1. 要求：必须拥有静态属性 contextType , 应赋值为创建的上下文对象
2. 在函数组件中，需要使用Consumer来获取上下文数据
   1. Consumer是一个组件
   2. 它的子节点，是一个函数（它的props.children需要传递一个函数）


**注意细节**

如果，上下文提供者（Context.Provider）中的value属性发生变化(Object.is比较)，会导致该上下文提供的所有后代元素全部重新渲染，无论该子元素是否有优化（无论shouldComponentUpdate函数返回什么结果）


# PureComponent

纯组件,用于避免不必要得渲染(运行render函数),从而提高效率

优化:如果一个组件的属性和状态，都没有发生变化，重新渲染该组件是没有必要的

PureComponent是一个组件,如果某个组件继承自该组件,则该组件的shouldComponentUpdate会进行优化,对属性和状态进行浅比较,如果相等则不会重新渲染

**注意**

1. PureComponent进行的是浅比较
   1. 为了效率,应该尽量使用PureComponent
   2. 要求不要改动之前的状态,永远是创建新的状态覆盖之前的状态(Immutable,不可变对象)
   3. 有一个第三方js库, Immutable.js,它专门用于制作不可变对象
2. 函数组件,使用React.memo函数制作纯组件

# render props

有时候，某些组件的各种功能及其处理逻辑几乎完全相同，只是显示的界面不一样，建议下面的方式认选其一来解决重复代码的问题（横切关注点）


1. render props
   1. 某个组件，需要某个属性
   2. 该属性是一个函数，函数的返回值用于渲染
   3. 函数的参数会传递为需要的数据
   4. 注意纯组件的属性（尽量避免每次传递的render props的地址不一致）
   5. 通常该属性的名字叫做render
2. HOC


# Portals

插槽:将一个React元素渲染到指定DOM容器中

ReactDOM.createPortal(React元素,真实得DOM容器),该函数返回一个React元素

**React得真实dom结构可以和虚拟结构有差异**

**注意事件冒泡**

1. React中的事件是包装过的
2. 它的事件冒泡是根据虚拟DOM树来冒泡的,与真实的DOM树无关。

# 错误边界

默认情况下，若一个组件在**渲染期间**（render）发生错误，会导致整个组件树全部被卸载

错误边界：是一个组件，该组件会捕获到渲染期间（render）子组件发生的错误，并有能力阻止错误继续传播

**让某个组件捕获错误**

1. 编写生命周期函数 getDerivedStateFromError
   1. 静态函数
   2. 运行时间点：渲染子组件的过程中，发生错误之后，在更新页面之前
   3. **注意：只有子组件发生错误，才会运行该函数**
   4. 该函数返回一个对象，React会将该对象的属性覆盖掉当前组件的state
   5. 参数：错误对象
   6. 通常，该函数用于改变状态
2. 编写生命周期函数 componentDidCatch
   1. 实例方法
   2. 运行时间点：渲染子组件的过程中，发生错误，更新页面之后，由于其运行时间点比较靠后，因此不太会在该函数中改变状态
   3. 通常，该函数用于记录错误消息

**细节**

某些错误，错误边界组件无法捕获

1. 自身的错误
2. 异步的错误
3. 事件中的错误

总结：仅处理渲染子组件期间的同步错误


# React中的事件

这里的事件：React内置的DOM组件中的事件

1. 给document注册事件
2. 几乎所有的元素的事件处理，均在document的事件中处理
   1. 一些不冒泡的事件，是直接在元素上监听
   2. 一些document上面没有的事件，直接在元素上监听
3. 在document的事件处理，React会根据虚拟DOM树的完成事件函数的调用
4. React的事件参数，并非真实的DOM事件参数，是React合成的一个对象，该对象类似于真实DOM的事件参数
   1. stopPropagation，阻止事件在虚拟DOM树中冒泡
   2. nativeEvent，可以得到真实的DOM事件对象
   3. 为了提高执行效率，React使用事件对象池来处理事件对象(同一个对象)


**注意事项**

1. 如果给真实的DOM注册事件，阻止了事件冒泡，则会导致react的相应事件无法触发
2. 如果给真实的DOM注册事件，事件会先于React事件运行
3. 通过React的事件中阻止事件冒泡，无法阻止真实的DOM事件冒泡
4. 可以通过nativeEvent.stopImmediatePropagation()，阻止document上剩余事件的执行
5. 在事件处理程序中，不要异步的使用事件对象，如果一定要使用，需要调用persist函数

# 渲染原理

渲染：生成用于显示的对象，以及将这些对象形成真实的DOM对象

- React元素：React Element，通过React.createElement创建（语法糖：JSX）
  - 例如：
  ```js
  <div><h1>标题</h1></div>
  <App />
  ```
- React节点：专门用于渲染到UI界面的对象，React会通过React元素，创建React节点，ReactDOM一定是通过React节点来进行渲染的
- 节点类型：
  - React DOM(ReactDOMComponent)节点：创建该节点的React元素类型是一个字符串
  - React 组件节点：创建该节点的React元素类型是一个函数或是一个类
  - React 文本节点：由字符串、数字创建的
  - React 空节点：由null、undefined、false、true
  - React 数组节点：该节点由一个数组创建
- 真实DOM：通过document.createElement创建的dom元素

![](2019-07-25-13-51-08.png)

## 首次渲染(新节点渲染)

1. 通过参数的值创建节点
2. 根据不同的节点，做不同的事情
   1. 文本节点：通过document.createTextNode创建真实的文本节点
   2. 空节点：什么都不做
   3. 数组节点：遍历数组，将数组每一项递归创建节点（回到第1步进行反复操作，直到遍历结束）
   4. DOM节点：通过document.createElement创建真实的DOM对象，然后立即设置该真实DOM元素的各种属性，然后遍历对应React元素的children属性，递归操作（回到第1步进行反复操作，直到遍历结束）
   5. 组件节点
      1. 函数组件：调用函数(该函数必须返回一个可以生成节点的内容)，将该函数的返回结果递归生成节点（回到第1步进行反复操作，直到遍历结束）
      2. 类组件：
         1. 创建该类的实例
         2. 立即调用对象的生命周期方法：static getDerivedStateFromProps
         3. 运行该对象的render方法，拿到节点对象（将该节点递归操作，回到第1步进行反复操作）
         4. 将该组件的componentDidMount加入到执行队列（先进先出，先进先执行），当整个虚拟DOM树全部构建完毕，并且将真实的DOM对象加入到容器中后，执行该队列
3. 生成出虚拟DOM树之后，将该树保存起来，以便后续使用
4. 将之前生成的真实的DOM对象，加入到容器中。

```js
const app = <div className="assaf">
    <h1>
        标题
        {["abc", null, <p>段落</p>]}
    </h1>
    <p>
        {undefined}
    </p>
</div>;
ReactDOM.render(app, document.getElementById('root'));
```

以上代码生成的虚拟DOM树：

![](2019-07-25-14-17-04.png)


```js

function Comp1(props) {
    return <h1>Comp1 {props.n}</h1>
}

function App(props) {
    return (
        <div>
            <Comp1 n={5} />
        </div>
    )
}

const app = <App />;
ReactDOM.render(app, document.getElementById('root'));
```

以上代码生成的虚拟DOM树：

![](2019-07-25-14-49-53.png)


```js
class Comp1 extends React.Component {
    render() {
        return (
            <h1>Comp1</h1>
        )
    }
}

class App extends React.Component {
    render() {
        return (
            <div>
                <Comp1 />
            </div>
        )
    }
}

const app = <App />;
ReactDOM.render(app, document.getElementById('root'));
```

以上代码生成的虚拟DOM树：

![](2019-07-25-14-56-35.png)

## 更新节点

更新的场景：

1. 重新调用ReactDOM.render，触发根节点更新
2. 在类组件的实例对象中调用setState，会导致该实例所在的节点更新

**节点的更新**

- 如果调用的是ReactDOM.render，进入根节点的**对比（diff）更新**
- 如果调用的是setState
  - 1. 运行生命周期函数，static getDerivedStateFromProps
  - 2. 运行shouldComponentUpdate，如果该函数返回false，终止当前流程 
  - 3. 运行render，得到一个新的节点，进入该新的节点的**对比更新**
  - 4. 将生命周期函数getSnapshotBeforeUpdate加入执行队列，以待将来执行
  - 5. 将生命周期函数componentDidUpdate加入执行队列，以待将来执行
 
后续步骤：
1. 更新虚拟DOM树
2. 完成真实的DOM更新
3. 依次调用执行队列中的componentDidMount
4. 依次调用执行队列中的getSnapshotBeforeUpdate
5. 依次调用执行队列中的componentDidUpdate


### 对比更新

将新产生的节点，对比之前虚拟DOM中的节点，发现差异，完成更新

问题：对比之前DOM树中哪个节点

React为了提高对比效率，做出以下假设

1. 假设节点不会出现层次的移动（对比时，直接找到旧树中对应位置的节点进行对比）
2. 不同的节点类型会生成不同的结构
   1. 相同的节点类型：节点本身类型相同，如果是由React元素生成，type值还必须一致
   2. 其他的，都属于不相同的节点类型
3. 多个兄弟通过唯一标识（key）来确定对比的新节点

key值的作用：用于通过旧节点，寻找对应的新节点，如果某个旧节点有key值，则其更新时，会寻找相同层级中的相同key值的节点，进行对比。

**key值应该在一个范围内唯一（兄弟节点中），并且应该保持稳定**

#### 找到了对比的目标

判断节点类型是否一致


- **一致**

根据不同的节点类型，做不同的事情

**空节点**：不做任何事情

**DOM节点**：
1. 直接重用之前的真实DOM对象
2. 将其属性的变化记录下来，以待将来统一完成更新（现在不会真正的变化）
3. 遍历该新的React元素的子元素，**递归对比更新**


**文本节点**：
1. 直接重用之前的真实DOM对象
2. 将新的文本变化记录下来，将来统一完成更新

**组件节点**：

**函数组件**：重新调用函数，得到一个节点对象，进入**递归对比更新**

**类组件**：

1. 重用之前的实例
2. 调用生命周期方法getDerivedStateFromProps
3. 调用生命周期方法shouldComponentUpdate，若该方法返回false，终止
4. 运行render，得到新的节点对象，进入**递归对比更新**
5. 将该对象的getSnapshotBeforeUpdate加入队列
6. 将该对象的componentDidUpdate加入队列

**数组节点**：遍历数组进行**递归对比更新**

- **不一致**

整体上，卸载旧的节点，全新创建新的节点

**创建新节点**

进入新节点的挂载流程

**卸载旧节点**

1. **文本节点、DOM节点、数组节点、空节点、函数组件节点**：直接放弃该节点，如果节点有子节点，递归卸载节点
2. **类组件节点**：
   1. 直接放弃该节点
   2. 调用该节点的componentWillUnMount函数
   3. 递归卸载子节点


#### 没有找到对比的目标

新的DOM树中有节点被删除

新的DOM树中有节点添加

- 创建新加入的节点
- 卸载多余的旧节点


# 工具

## 严格模式

StrictMode(``React.StrictMode``)，本质是一个组件，该组件不进行UI渲染（``React.Fragment <> </>``），它的作用是，在渲染内部组件时，发现不合适的代码。

- 识别不安全的生命周期
- 关于使用过时字符串 ref API 的警告
- 关于使用废弃的 findDOMNode 方法的警告
- 检测意外的副作用
  - React要求，副作用代码仅出现在以下生命周期函数中
  - 1. ComponentDidMount
  - 2. ComponentDidUpdate
  - 3. ComponentWillUnMount

副作用：一个函数中，做了一些会影响函数外部数据的事情，例如：

1. 异步处理
2. 改变参数值
3. setState
4. 本地存储
5. 改变函数外部的变量

相反的，如果一个函数没有副作用，则可以认为该函数是一个纯函数

在严格模式下，虽然不能监控到具体的副作用代码，**但它会将具有副作用的函数调用两遍**，以便发现问题。（这种情况，仅在开发模式下有效）

- 检测过时的 context API

## Profiler

性能分析工具

分析某一次或多次提交（更新），涉及到的组件的渲染时间

火焰图：得到某一次提交，每个组件总的渲染时间以及自身的渲染时间

排序图：得到某一次提交，每个组件自身渲染时间的排序

组件图：某一个组件，在多次提交中，自身渲染花费的时间

# HOOK简介

HOOK是React16.8.0之后出现

组件：无状态组件（函数组件）、类组件

类组件中的麻烦：

1. this指向问题

2. 繁琐的生命周期

3. 其他问题

HOOK专门用于增强函数组件的功能（HOOK在类组件中是不能使用的），使之理论上可以成为类组件的替代品

官方强调：没有必要更改已经完成的类组件，官方目前没有计划取消类组件，只是鼓励使用函数组件

HOOK（钩子）本质上是一个函数(命名上总是以use开头)，该函数可以挂载任何功能

HOOK种类：

1. useState
2. useEffect
3. 其他...

## State Hook

State Hook是一个在函数组件中使用的函数（useState），用于在函数组件中使用状态

useState

- 函数有一个参数，这个参数的值表示状态的默认值
- 函数的返回值是一个数组，该数组一定包含两项
  - 第一项：当前状态的值
  - 第二项：改变状态的函数

一个函数组件中可以有多个状态，这种做法非常有利于横向切分关注点。

**核心原理**
```js
export default function App(){
    const [N, setN] = useState(0);
    const [visible, setVisible] = useState(true)
    return <div>
        <p style={{display:visible?"block":'none'}}>
            <button onClick={()=>{
                setN(N-1)
            }}>-</button>
            <span>{N}</span>
            <button onClick={()=>{
                setN(N+1)
            }}>+</button>
        </p>
        <button onClick={()=>{
            setVisible(!visible)
        }}>显示/隐藏</button>
    </div>
}
```
![](hook核心原理.png)

**注意的细节**

1. useState最好写到函数的起始位置，便于阅读
2. useState严禁出现在代码块（判断、循环）中
3. useState返回的函数（数组的第二项），引用不变（节约内存空间）
4. 使用函数改变数据，若数据和之前的数据完全相等（使用Object.is比较），不会导致重新渲染，以达到优化效率的目的。
5. 使用函数改变数据，传入的值不会和原来的数据进行合并，而是直接替换。
6. 如果要实现强制刷新组件
   1. 类组件：使用forceUpdate函数
   2. 函数组件：使用一个空对象的useState
7. **如果某些状态之间没有必然的联系，应该分化为不同的状态，而不要合并成一个对象**
8. 和类组件的状态一样，函数组件中改变状态可能是异步的（在DOM事件中），多个状态变化会合并以提高效率，此时，不能信任之前的状态，而应该使用回调函数的方式改变状态。如果状态变化要使用到之前的状态，尽量传递函数。

## Effect Hook

Effect Hook：用于在函数组件中处理副作用

副作用：

1. ajax请求
2. 计时器
3. 其他异步操作
4. 更改真实DOM对象
5. 本地存储
6. 其他会对外部产生影响的操作

函数：useEffect，该函数接收一个函数作为参数，接收的函数就是需要进行副作用操作的函数

**细节**

1. 副作用函数的运行时间点，是在页面完成真实的UI渲染之后。因此它的执行是异步的，并且不会阻塞浏览器
   1. 与类组件中componentDidMount和componentDidUpdate的区别
   2. componentDidMount和componentDidUpdate，更改了真实DOM，但是用户还没有看到UI更新，同步的。
   3. useEffect中的副作用函数，更改了真实DOM，并且用户已经看到了UI更新，异步的。
2. 每个函数组件中，可以多次使用useEffect，但不要放入判断或循环等代码块中。
3. useEffect中的副作用函数，可以有返回值，返回值必须是一个函数，该函数叫做清理函数
   1. 该函数运行时间点，在每次运行副作用函数之前
   2. 首次渲染组件不会运行
   3. 组件被销毁时一定会运行
4. useEffect函数，可以传递第二个参数
   1. 第二个参数是一个数组
   2. 数组中记录该副作用的依赖数据
   3. 当组件重新渲染后，只有依赖数据与上一次不一样的时，才会执行副作用
   4. 所以，当传递了依赖数据之后，如果数据没有发生变化
      1. 副作用函数仅在第一次渲染后运行
      2. 清理函数仅在卸载组件后运行
5. 副作用函数中，如果使用了函数上下文中的变量，则由于闭包的影响，会导致副作用函数中变量不会实时变化。
6. 副作用函数在每次注册时，会覆盖掉之前的副作用函数，因此，尽量保持副作用函数稳定，否则控制起来会比较复杂。


## 自定义HOOK

State Hook： useState
Effect Hook：useEffect

自定义Hook：将一些常用的、跨越多个组件的Hook功能，抽离出去形成一个函数，该函数就是自定义Hook，自定义Hook，由于其内部需要使用Hook功能，所以它本身也需要按照Hook的规则实现：

1. 函数名必须以use开头
2. 调用自定义Hook函数时，应该放到顶层

例如：

1. 很多组件都需要在第一次加载完成后，获取所有学生数据
2. 很多组件都需要在第一次加载完成后，启动一个计时器，然后在组件销毁时卸载

> 使用Hook的时候，如果没有严格按照Hook的规则进行，eslint的一个插件（eslint-plugin-react-hooks）会报出警告

## Reducer Hook

Flux：Facebook出品的一个数据流框架

1. 规定了数据是单向流动的
2. 数据存储在数据仓库中（目前，可以认为state就是一个存储数据的仓库）
3. action是改变数据的唯一原因（本质上就是一个对象，action有两个属性）
   1. type：字符串，动作的类型
   2. payload：任意类型，动作发生后的附加信息
   3. 例如，如果是添加一个学生，action可以描述为：
      1. ```{ type:"addStudent", payload: {学生对象的各种信息} }```
   4. 例如，如果要删除一个学生，action可以描述为：
      1. ```{ type:"deleteStudent", payload: 学生id }```
4. 具体改变数据的是一个函数，该函数叫做reducer
   1. 该函数接收两个参数
      1. state：表示当前数据仓库中的数据
      2. action：描述了如何去改变数据，以及改变数据的一些附加信息
   2. 该函数必须有一个返回结果，用于表示数据仓库变化之后的数据
      1. Flux要求，对象是不可变的，如果返回对象，必须创建新的对象
   3. reducer必须是纯函数，不能有任何副作用
5. 如果要触发reducer，不可以直接调用，而是应该调用一个辅助函数dispatch
   1. 该函数仅接收一个参数：action
   2. 该函数会间接去调用reducer，以达到改变数据的目的

## Context Hook

用户获取上下文数据

## Callback Hook

函数名：useCallback

用于得到一个固定引用值的函数，通常用它进行性能优化

useCallback:

该函数有两个参数：

1. 函数，useCallback会固定该函数的引用，只要依赖项没有发生变化，则始终返回之前函数的地址
2. 数组，记录依赖项

该函数返回：引用相对固定的函数地址

## Memo Hook

用于保持一些比较稳定的数据，通常用于性能优化

**如果React元素本身的引用没有发生变化，一定不会重新渲染**

## Ref Hook

useRef函数：

1. 一个参数：默认值
2. 返回一个固定的对象，```{current: 值}```

## ImperativeHandle Hook

函数：useImperativeHandleHook

有时候我们希望再类组件中调用一个方法,我们往往是通过ref的方式来调用,如果是函数组件呢,这个时候useImperativeHandleHook就起作用了.

由于函数组件本身无法接受ref,可以利用ref转发,把ref传进来.

useImperativeHandleHook,接受3个参数
- ref 第一个ref
- 一个函数,函数的返回值赋给ref
- 依赖项,如果没有依赖项,则函数运行每次都会调用,使用了依赖项,则第一次调用后会缓存,只有依赖项发生变化才会重新调用.

## LayoutEffect Hook

useEffect：浏览器渲染完成后，用户看到新的渲染结果之后

useLayoutEffectHook：完成了DOM改动，但还没有呈现给用户

应该尽量使用useEffect，因为它不会导致渲染阻塞，如果出现了问题，再考虑使用useLayoutEffectHook

## DebugValue Hook

useDebugValue：用于将自定义Hook的关联数据显示到调试栏
如果创建的自定义Hook通用性比较高，可以选择使用useDebugValue方便调试

# React动画

React动画库：react-transition-group


## CSSTransition

当进入时，发生：

1. 为CSSTransition内部的DOM根元素（后续统一称之为DOM元素）添加样式enter
2. 在一下帧(enter样式已经完全应用到了元素)，立即为该元素添加样式enter-active
3. 当timeout结束后，去掉之前的样式，添加样式enter-done

当退出时，发生：

1. 为CSSTransition内部的DOM根元素（后续统一称之为DOM元素）添加样式exit
2. 在一下帧(exit样式已经完全应用到了元素)，立即为该元素添加样式exit-active
3. 当timeout结束后，去掉之前的样式，添加样式exit-done

设置classNames属性，可以指定类样式的名称

1. 字符串：为类样式添加前缀
2. 对象：为每个类样式指定具体的名称（非前缀）


关于首次渲染时的类样式，appear、apear-active、apear-done，它和enter的唯一区别在于完成时，会同时加入apear-done和enter-done


还可以与Animate.css联用

## SwitchTransition

用于有秩序的切换内部组件

默认情况下：out-in

1. 当key值改变时，会将之前的DOM根元素添加退出样式（exit,exit-active)
2. 退出完成后，将该DOM元素移除
3. 重新渲染内部DOM元素
4. 为新渲染的DOM根元素添加进入样式(enter, enter-active, enter-done)

in-out:
1. 重新渲染内部DOM元素，保留之前的元素
2. 为新渲染的DOM根元素添加进入样式(enter, enter-active, enter-done)
3. 将之前的DOM根元素添加退出样式（exit,exit-active)
4. 退出完成后，将该DOM元素移除

> 该库寻找dom元素的方式，是使用已经过时的API：findDomNode，该方法可以找到某个组件下的DOM根元素


## TransitionGroup

该组件的children，接收多个Transition或CSSTransition组件，该组件用于根据这些子组件的key值，控制他们的进入和退出状态

# React Router 

## 概述

React路由

## 站点

![](/images/2019-08-02-14-40-44.png)

无论是使用Vue，还是React，开发的单页应用程序，可能只是该站点的一部分（某一个功能块）

一个单页应用里，可能会划分为多个页面（几乎完全不同的页面效果）（组件）

如果要在单页应用中完成组件的切换，需要实现下面两个功能：

1. 根据不同的页面地址，展示不同的组件（核心）
2. 完成无刷新的地址切换

我们把实现了以上两个功能的插件，称之为路由

## React Router

1. react-router：路由核心库，包含诸多和路由功能相关的核心代码
2. react-router-dom：利用路由核心库，结合实际的页面，实现跟页面路由密切相关的功能

如果是在页面中实现路由，需要安装react-router-dom库


## 两种模式

路由：根据不同的页面地址，展示不同的组件

url地址组成

例：https://www.react.com:443/news/1-2-1.html?a=1&b=2#abcdefg

1. 协议名(schema)：https
2. 主机名(host)：www.react.com
   1. ip地址
   2. 预设值：localhost
   3. 域名
   4. 局域网中电脑名称
3. 端口号(port)：443
   1. 如果协议是http，端口号是80，则可以省略端口号
   2. 如果协议是https，端口号是443，则可以省略端口号
4. 路径(path)：/news/1-2-1.html
5. 地址参数(search、query)：?a=1&b=2
   1. 附带的数据
   2. 格式：属性名=属性值&属性名=属性值....
6. 哈希(hash、锚点)
   1. 附带的数据

### Hash Router 哈希路由

根据url地址中的哈希值来确定显示的组件

> 原因：hash的变化，不会导致页面刷新
> 这种模式的兼容性最好

### Borswer History Router 浏览器历史记录路由

HTML5出现后，新增了History Api，从此以后，浏览器拥有了改变路径而不刷新页面的方式

History表示浏览器的历史记录，它使用栈的方式存储。


![](/images/2019-08-02-15-24-05.png)
1. history.length：获取栈中数据量
2. history.pushState：向当前历史记录栈中加入一条新的记录
   1. 参数1：附加的数据，自定义的数据，可以是任何类型
   2. 参数2：页面标题，目前大部分浏览器不支持
   3. 参数3：新的地址
3. history.replaceState：将当前指针指向的历史记录，替换为某个记录
   1. 参数1：附加的数据，自定义的数据，可以是任何类型
   2. 参数2：页面标题，目前大部分浏览器不支持
   3. 参数3：新的地址

根据页面的路径决定渲染哪个组件


## 路由组件
React-Router 为我们提供了两个重要组件
### Router组件

它本身不做任何展示，仅提供路由模式配置，另外，该组件会产生一个上下文，上下文中会提供一些实用的对象和方法，供其他相关组件使用

1. HashRouter：该组件，使用hash模式匹配
2. BrowserRouter：该组件，使用BrowserHistory模式匹配

### Route组件

根据不同的地址，展示不同的组件

重要属性：

1. path：匹配的路径
   1. 默认情况下，不区分大小写，可以设置sensitive属性为true，来区分大小写
   2. 默认情况下，只匹配初始目录，如果要精确匹配，配置exact属性为true
   3. 如果不写path，则会匹配任意路径
2. component：匹配成功后要显示的组件
3. children：
   1. **传递React元素，无论是否匹配，一定会显示children，并且会忽略component属性**目前版本有问题，待查
   2. 传递一个函数，该函数有多个参数，这些参数来自于上下文，该函数返回react元素，则一定会显示返回的元素，并且忽略component属性

Route组件可以写到任意的地方，只要保证它是Router组件的后代元素

### Switch组件

写到Switch组件中的Route组件，当匹配到第一个Route后，会立即停止匹配

由于Switch组件会循环所有子元素，然后让每个子元素去完成匹配，若匹配到，则渲染对应的组件，然后停止循环。因此，不能在Switch的子元素中使用除Route外的其他组件。

## 路由信息

Router组件会创建一个上下文，并且，向上下文中注入一些信息

该上下文对开发者是隐藏的，Route组件若匹配到了地址，则会将这些上下文中的信息作为属性传入对应的组件

### history

它并不是window.history对象，我们利用该对象无刷新跳转地址

**为什么没有直接使用history对象**

1. React-Router中有两种模式：Hash、History，如果直接使用window.history，只能支持一种模式
2. 当使用windows.history.pushState方法时，没有办法收到任何通知，将导致React无法知晓地址发生了变化，结果导致无法重新渲染组件

- push：将某个新的地址入栈（历史记录栈）
  - 参数1：新的地址
  - 参数2：可选，附带的状态数据
- replace：将某个新的地址替换掉当前栈中的地址
- go: 与window.history一致
- forward: 与window.history一致
- back: 与window.history一致

### location

与history.location完全一致，是同一个对象，但是，与window.location不同

location对象中记录了当前地址的相关信息

我们通常使用第三方库```query-string```，用于解析地址栏中的数据

### match

该对象中保存了，路由匹配的相关信息

- isExact：事实上，当前的路径和路由配置的路径是否是精确匹配的
- params：获取路径规则中对应的数据

实际上，在书写Route组件的path属性时，可以书写一个```string pattern```（字符串正则）

react-router使用了第三方库：Path-to-RegExp，该库的作用是，将一个字符串正则转换成一个真正的正则表达式。

**向某个页面传递数据的方式：**

1. 使用state：在push页面时，加入state
2. **利用search：把数据填写到地址栏中的？后**
3. 利用hash：把数据填写到hash后
4. **params：把数据填写到路径中**

### 非路由组件获取路由信息

某些组件，并没有直接放到Route中，而是嵌套在其他普通组件中，因此，它的props中没有路由信息，如果这些组件需要获取到路由信息，可以使用下面两种方式：


1. 将路由信息从父组件一层一层传递到子组件
2. 使用react-router提供的高阶组件withRouter，包装要使用的组件，该高阶组件会返回一个新组件，新组件将向提供的组件注入路由信息。

## 其他组件

已学习：

- Router：BrowswerRouter、HashRouter
- Route
- Switch
- 高阶函数：withRouter

### Link

生成一个无刷新跳转的a元素

- to
  - 字符串：跳转的目标地址
  - 对象：
    - pathname：url路径
    - search
    - hash
    - state：附加的状态信息
- replace：bool，表示是否是替换当前地址，默认是false
- innerRef：可以将内部的a元素的ref附着在传递的对象或函数参数上
  - 函数
  - ref对象

### NavLink

是一种特殊的Link，Link组件具备的功能，它都有

它具备的额外功能是：根据当前地址和链接地址，来决定该链接的样式

- activeClassName: 匹配时使用的类名
- activeStyle: 匹配时使用的内联样式
- exact: 是否精确匹配
- sensitive：匹配时是否区分大小写
- strict：是否严格匹配最后一个斜杠

### Redirect

重定向组件，当加载到该组件时，会自动跳转（无刷新）到另外一个地址

- to：跳转的地址
  - 字符串
  - 对象
- push: 默认为false，表示跳转使用替换的方式，设置为true后，则使用push的方式跳转
- from：当匹配到from地址规则时才进行跳转
- exact: 是否精确匹配from
- sensitive：from匹配时是否区分大小写
- strict：from是否严格匹配最后一个斜杠



## 导航守卫

导航守卫：当离开一个页面，进入另一个页面时，触发的事件

history对象
- listen: 添加一个监听器，监听地址的变化，当地址发生变化时，会调用传递的函数
  - 参数：函数，运行时间点：发生在即将跳转到新页面时
    - 参数1：location对象，记录当前的地址信息
    - 参数2：action，一个字符串，表示进入该地址的方式
      - POP：出栈
        - 通过点击浏览器后退、前进
        - 调用history.go
        - 调用history.goBack
        - 调用history.goForward
      - PUSH：入栈
        - history.push
      - REPLACE：替换
        - history.replace
  - 返回结果：函数，可以调用该函数取消监听
- block：设置一个阻塞，并同时设置阻塞消息，当页面发生跳转时，会进入阻塞，并将阻塞消息传递到路由根组件的getUserConfirmation方法。
  - 返回一个回调函数，用于取消阻塞器

路由根组件

- getUserConfirmation
  - 参数：函数
    - 参数1：阻塞消息
      - 字符串消息
      - 函数，函数的返回结果是一个字符串，用于表示阻塞消息
        - 参数1：location对象
        - 参数2：action值
    - 参数2：回调函数，调用该函数并传递true，则表示进入到新页面，否则，不做任何操作


## 常见应用 - 路由切换动画

第三方动画库：react-transition-group

CSSTransition：用于为内部的DOM元素添加类样式，通过in属性决定内部的DOM处于退出还是进入阶段。

## 常见应用 - 滚动条复位

- 高阶组件
- 使用useeffect
- 使用自定义的导航守卫

# React Router源码

## path-to-regexp

**创建一个match对象**

第三方库：path-to-regexp，用于将一个字符串正则（路径正则，path regexp）转换为正则.

**React中Route的exact属性,对应为path-to-regexp中的end(是否匹配到字符串的结尾)配置.**

**React中match对象的isExact属性,当正则匹配到的部分和输入的字符串地址一致是,为true**

## history对象

该对象提供了一些方法，用于控制或监听地址的变化。

该对象**不是**window.history，而是一个抽离的对象，它提供统一的API接口，封装了具体的实现

- createBrowserHistory  产生的控制浏览器真实地址的history对象
- createHashHistory  产生的控制浏览器hash的history对象
- createMemoryHistory  产生的控制内存中地址数组的history对象

history对象共同的特点：维护了一个地址栈

第三方库：history

**以下三个函数，虽然名称和参数不同，但返回的对象结构(history)完全一致**

- action：当前地址栈，最后一次操作的类型
  - 如果是通过createXXXHistory函数新创建的history对象，action固定为POP
  - 如果调用了history的push方法，action变为PUSH
  - 如果调用了history的replace方法，action变为REPLACE
- push：向当前地址栈指针位置，入栈一个地址
- replace：替换指针指向的地址
- go：控制当前地址栈指针偏移，如果是0，地址不变；如果是负数，则后退指定的步数；如果是正数，则前进指定的步数；
- back：相当于go(-1)
- forward：相当于go(1)
- location：表达当前地址中的信息
- listen：函数，用于监听地址栈指针的变化
  - 该函数接收一个函数作为参数，该参数表示地址变化后要做的事情
    - 参数函数接收两个参数
    - location：记录了新的地址
    - action：进入新地址的方式
      - POP：指针移动，调用go、goBack、goForward、用户点击浏览器后退按钮    
      - PUSH：调用history.push
      - REPLACE：调用history.replace
  - 该函数有一个返回值，返回的是一个函数，用于取消监听
- block：用于设置一个阻塞，返回取消阻塞函数.
  - 参数为一个对象
    - retry:调用该函数会进行再次跳转地址.
  - 设置阻塞后,通过验证之后,可以先调用阻塞函数,在调用retry实现跳转。


### createBrowserHistory

创建一个使用浏览器History Api的history对象

### createHashHistory

创建一个使用浏览器hash的history对象


### createMemoryHistory

创建一个使用内存中的地址栈的history对象，一般用于没有地址栏的环境
