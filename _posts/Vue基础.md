---
title: Vue基础
date: 2019-09-09 11:29:01
tags: 
- Vue
categories: 前端框架
description: 依据Vue官方文档记录，加深理解。
---

# Vue整体介绍

## 安装

直接下载,script标签引入，vue会被注册为一个全局变量

```javascript
<script src="vue.js"></script>
```

## Hello Vue!

```html
<div id="app">
    {{message}}
</div>

<script>
    var app = new Vue({
        el: '#app',
        data: {
            message: 'Hello Vue!'
        }
    })
</script>

结果>>
Hello Vue
```

## 声明式渲染

如上Hello Vue，现在数据和 DOM 已经被建立了关联，所有东西都是响应式的。如下修改app.message的值，页面对应会发生变化

![](stack.gif)

除了文本插值，我们还可以像这样来绑定元素特性：

```html
<div id="app">
    <span v-bind:title='message'>
        鼠标悬停几秒钟查看此处动态绑定的提示信息！
    </span>
</div>

<script>
    var app = new Vue({
        el: '#app',
        data: {
            message: '页面加载于' + new Date().toLocaleString()
        }
    })
</script>

```
你看到的 v-bind 特性被称为指令。指令带有前缀 v-，以表示它们是 Vue 提供的特殊特性。在这里，该指令的意思是：“将这个元素节点的 title 特性和 Vue 实例的 message 属性保持一致”。


## 条件与循环

```html
<div id="app">
    <p v-if='seen'>现在你看到我了</p>
</div>
<script>
    var vm = new Vue({
        el: '#app',
        data: {
            seen: true
        }
    });
</script>
```

这个例子演示了我们不仅可以把数据绑定到 DOM 文本或特性，还可以绑定到 DOM 结构。

```html
<div id="app">
    <ol>
        <li v-for='todo in todos'>
            {{todo.text}}
        </li>
    </ol>
</div>
<script>
    var vm = new Vue({
        el: '#app',
        data: {
            todos: [
                { text: '学习 JavaScript' },
                { text: '学习 Vue' },
                { text: '整个牛项目' }
            ]
        }
    });
</script>
```

还有其它很多指令，每个都有特殊的功能。例如，v-for 指令可以绑定数组的数据来渲染一个项目列表：

## 处理用户输入

为了让用户和你的应用进行交互，我们可以用 v-on 指令添加一个事件监听器，通过它调用在 Vue 实例中定义的方法：


```html
<div id="app">
    <p>{{message}}</p>
    <button v-on:click='reverseMessage'>反转消息</button>

</div>

<script>
    var vm = new Vue({
        el: '#app',
        data: {
            message: 'Hello Vue.js!'
        },
        methods: {
            reverseMessage: function () {
                this.message = this.message.split('').reverse().join('')
            }
        }
    });
</script>

结果>>
!sj.euV olleH
```


Vue 还提供了 v-model 指令，它能轻松实现表单输入和应用状态之间的双向绑定.


```html
<div id="app">
    <p>{{message}}</p>
    <input v-model='message' type="text">
</div>

<script>
    var vm = new Vue({
        el: '#app',
        data: {
            message: 'Hello Vue!'
        }
    });
</script>
```

## 组件化应用构建

组件系统是 Vue 的另一个重要概念，因为它是一种抽象，允许我们使用小型、独立和通常可复用的组件构建大型应用。

```html
<div id="app">
    <ol>
        <button-counter></button-counter>
    </ol>
</div>
<script>
    Vue.component('button-counter', {
        template: '<li>这是个待办项</li>'
    });
    var vm = new Vue({
        el: '#app'
    });
</script>
```

**先注册组件，在实例化Vue**

**组件名称为小写**


```html
<div id="app">
    <ol>
        <todo-item v-for='item in groceryList' v-bind:todo='item' v-bind:key='item.id'></todo-item>
    </ol>
</div>

<script>
    Vue.component('todo-item', {
        props: ['todo'],
        template: '<li>{{todo.text}}</li>'
    });
    var vm = new Vue({
        el: '#app',
        data: {
            groceryList: [
                { id: 0, text: '蔬菜' },
                { id: 1, text: '奶酪' },
                { id: 2, text: '随便其它什么人吃的东西' }
            ]
        }
    })
</script>
```

todo-item 组件现在接受一个"prop"，类似于一个自定义特性。这个 prop 名为 todo。通过v-bind:todo给todo赋值，然后动态获取text值，设置到li的text中

# Vue实例

## 创建一个Vue实例

```javascript
var vm = new Vue({
  // 选项
})
```

## 数据与方法

当一个 Vue 实例被创建时，它将 data 对象中的所有的属性加入到 Vue 的响应式系统中。当这些属性的值发生改变时，视图将会产生“响应”，即匹配更新为新的值

```javascript

// 我们的数据对象
var data = { a: 1 }

// 该对象被加入到一个 Vue 实例中
var vm = new Vue({
  data: data
})

// 获得这个实例上的属性
// 返回源数据中对应的字段
vm.a == data.a // => true

// 设置属性也会影响到原始数据
vm.a = 2
data.a // => 2

// ……反之亦然
data.a = 3
vm.a // => 3

```

当这些数据改变时，视图会进行重渲染。值得注意的是只有当实例被创建时就已经存在于 data 中的属性才是响应式的。也就是说如果你添加一个新的属性，比如：

```javascript
vm.b = 'hi'
```

那么对 b 的改动将不会触发任何视图的更新。如果你知道你会在晚些时候需要一个属性，但是一开始它为空或不存在，那么你仅需要设置一些初始值。比如：

```javascript
data: {
  newTodoText: '',
  visitCount: 0,
  hideCompletedTodos: false,
  todos: [],
  error: null
}
```

这里唯一的例外是使用 Object.freeze()，这会阻止修改现有的属性，也意味着响应系统无法再追踪变化。

```javascript
var obj = {
  foo: 'bar'
}

Object.freeze(obj)

new Vue({
  el: '#app',
  data: obj
})

<div id="app">
  <p>{{ foo }}</p>
  <!-- 这里的 `foo` 不会更新！ -->
  <button v-on:click="foo = 'baz'">Change it</button>
</div>

```

除了数据属性，Vue 实例还暴露了一些有用的实例属性与方法。它们都有前缀 $，以便与用户定义的属性区分开来。例如：

```javascript
var data = { a: 1 }
var vm = new Vue({
  el: '#example',
  data: data
})

vm.$data === data // => true
vm.$el === document.getElementById('example') // => true

// $watch 是一个实例方法
vm.$watch('a', function (newValue, oldValue) {
  // 这个回调将在 `vm.a` 改变后调用
})
```

## 实例生命周期钩子

每个 Vue 实例在被创建时都要经过一系列的初始化过程——例如，需要设置数据监听、编译模板、将实例挂载到 DOM 并在数据变化时更新 DOM 等。同时在这个过程中也会运行一些叫做生命周期钩子的函数，这给了用户在不同阶段添加自己的代码的机会。

```javascript
<div id="app">
    {{msg}}
</div>

<script>
    var vm = new Vue({
        el: '#app',
        data: {
            msg: 'hi vue'
        },
        //在实例化之后,数据观测和event事件配置之前被调用
        beforeCreate: function () {
            console.log('beforeCreate');
        },
        //在实例创建完成后被立即调用。
        //在这一步，实例已完成以下的配置：数据观测 (data observer)，属性和方法的运算，watch/event 事件回调。
        //然而，挂载阶段还没开始，$el 属性目前不可见。
        created: function () {
            console.log('created')
        },

        //在挂载开始之前被调用：相关的 render 函数首次被调用。
        beforeMount: function () {
            console.log('beforeMount')
        },
        //el 被新创建的 vm.$el 替换，挂载成功
        mounted: function () {
            console.log('mounted');
        },
        //数据更新时调用
        beforeUpdate: function () {
            console.log('beforeUpdate')
        },
        //组件Dom已经更新,组件更新完毕
        updated: function () {
            console.log('updated')
        }
    });
    setTimeout(() => {
        vm.msg = '改变中....';
    }, 300);
</script>
```

贴一张官网示例图如下:

![](lifecycle.png)

# 模板语法

## 文本

数据绑定最常见的形式就是使用“Mustache”语法 (双大括号) 的文本插值：

``` html
<span>Message: {{ msg }}</span>
```

Mustache与数据对象上msg属性的值，msg发生改变，则Mustanche里的的值也会变

通过使用 v-once 指令，你也能执行一次性地插值，当数据改变时，插值处的内容不会更新。但请留心这会影响到该节点上的其它数据绑定：

```html

<span v-once>这个将不会改变: {{ msg }}</span>

```

## 原始HTML

双大括号会将数据解释为普通文本，而非 HTML 代码。为了输出真正的 HTML，你需要使用 v-html 指令：

```html
<div id="app">
    {{rawHtml}}
    <p v-html='rawHtml' v-bind:id='text'></p>
</div>

<script>
    var data = { a: 1, rawHtml: '<span style="color:red">123</span>', text: 'csid' }
    var vm = new Vue({
        el: '#app',
        data: data,
    })
</script>
```

## 特性

Mustache 语法不能作用在 HTML 特性上，遇到这种情况应该使用 v-bind 指令：

```html
<div v-bind:id="dynamicId"></div>
```

对于布尔特性 (它们只要存在就意味着值为 true)，v-bind 工作起来略有不同，在这个例子中：

```html
<button v-bind:disabled="isButtonDisabled">Button</button>
```

如果 isButtonDisabled 的值是 null、undefined 或 false，则 disabled 特性甚至不会被包含在渲染出来的 <button> 元素中。


## 使用 JavaScript 表达式

迄今为止，在我们的模板中，我们一直都只绑定简单的属性键值。但实际上，对于所有的数据绑定，Vue.js 都提供了完全的 JavaScript 表达式支持。

```javascript

{{ number + 1 }}

{{ ok ? 'YES' : 'NO' }}

{{ message.split('').reverse().join('') }}

<div v-bind:id="'list-' + id"></div>

```

这些表达式会在所属 Vue 实例的数据作用域下作为 JavaScript 被解析。有个限制就是，每个绑定都只能包含单个表达式，所以下面的例子都不会生效。

```html

<!-- 这是语句，不是表达式 -->
{{ var a = 1 }}

<!-- 流控制也不会生效，请使用三元表达式 -->
{{ if (ok) { return message } }}

```

## 指令

指令 (Directives) 是带有 v- 前缀的特殊特性。指令特性的值预期是单个 JavaScript 表达式 (v-for 是例外情况，稍后我们再讨论)。指令的职责是，当表达式的值改变时，将其产生的连带影响，响应式地作用于 DOM。回顾我们在介绍中看到的例子

```html
<p v-if="seen">现在你看到我了</p>

```

## 参数

一些指令能够接收一个“参数”，在指令名称之后以冒号表示。例如，v-bind 指令可以用于响应式地更新 HTML 特性：

```html

//在这里 href 是参数，告知 v-bind 指令将该元素的 href 特性与表达式 url 的值绑定。
<a v-bind:href="url">...</a>

```

另一个例子是 v-on 指令，它用于监听 DOM 事件：

```html
<a v-on:click="doSomething">...</a>
```


## 修饰符

修饰符 (modifier) 是以半角句号 . 指明的特殊后缀，用于指出一个指令应该以特殊方式绑定。例如，.prevent 修饰符告诉 v-on 指令对于触发的事件调用 event.preventDefault()：

```html

<form v-on:submit.prevent="onSubmit">...</form>

```

## 缩写

1. v-bind 缩写

```javascript

<!-- 完整语法 -->
<a v-bind:href="url">...</a>

<!-- 缩写 -->
<a :href="url">...</a>

```
2. v-on 缩写

```javascript

<!-- 完整语法 -->
<a v-on:click="doSomething">...</a>

<!-- 缩写 -->
<a @click="doSomething">...</a>

```

## 计算属性和侦听器

### 基础例子

模板内的表达式非常便利，但是设计它们的初衷是用于简单运算的。在模板中放入太多的逻辑会让模板过重且难以维护。例如：

```html
<div id="example">
  {{ message.split('').reverse().join('') }}
</div>
```


```html
<div id="example">
    <p>Original message:{{message}}</p>
    <p>Computed reversed message:{{reversedMessage }}</p>
</div>

<script>
    var vm = new Vue({
        el: '#example',
        data: {
            message: 'hello'
        },
        computed: {
            reversedMessage: function () {
               
                return this.message.split('').reverse().join('')
            }
        }
    });

</script>
```

这里我们声明了一个计算属性 reversedMessage。我们提供的函数将用作属性 vm.reversedMessage 的 getter 函数

你可以像绑定普通属性一样在模板中绑定计算属性。Vue 知道 vm.reversedMessage 依赖于 vm.message，因此当 vm.message 发生改变时，所有依赖 vm.reversedMessage 的绑定也会更新。

### 计算属性vs方法

```javascript

<script>
    var vm = new Vue({
        el: '#example',
        data: {
            message: 'hello'
        },
        computed: {
            reversedMessage: function () {
                return this.message.split('').reverse().join('')
            },
            now: function () {
                return Date.now()
            }
        },
        methods: {
            reversedMessage2: function () {
                return this.message.split('').reverse().join('')
            }
        }
    });

</script>

```

我们可以将同一函数定义为一个方法而不是一个计算属性。两种方式的最终结果确实是完全相同的。然而，不同的是计算属性是基于它们的响应式依赖进行缓存的。

只在相关响应式依赖发生改变时它们才会重新求值。这就意味着只要 message 还没有发生改变，多次访问 reversedMessage 计算属性会立即返回之前的计算结果，而不必再次执行函数。

如上
>计算属性now每次调用不会更新，因为他不是响应式依赖
>方法reversedMessage2每次使用都会调用
>计算属性reversedMessage依赖message的改变，才会调用，对计算结果进行了缓存


### 计算属性vs侦听属性

Vue 提供了一种更通用的方式来观察和响应 Vue 实例上的数据变动：侦听属性。当你有一些数据需要随着其它数据变动而变动时，你很容易滥用 watch

细想一下这个例子

```javascript
<div id="demo">{{ fullName }}</div>

var vm = new Vue({
  el: '#demo',
  data: {
    firstName: 'Foo',
    lastName: 'Bar',
    fullName: 'Foo Bar'
  },
  watch: {
    firstName: function (val) {
      this.fullName = val + ' ' + this.lastName
    },
    lastName: function (val) {
      this.fullName = this.firstName + ' ' + val
    }
  }
})
```

上面代码是命令式且重复的。将它与计算属性的版本进行比较：

```javascript

var vm = new Vue({
  el: '#demo',
  data: {
    firstName: 'Foo',
    lastName: 'Bar'
  },
  computed: {
    fullName: function () {
      return this.firstName + ' ' + this.lastName
    }
  }
})
```

舒服多了

### 计算属性的setter

计算属性默认只有 getter ，不过在需要时你也可以提供一个 setter ：

```javascript
----
computed: {
    reversedMessage3: {
        get: function () {
            return this.message.split('').reverse().join('')
        },
        set: function (newvalue) {
            this.message = newvalue
        }
    }
},
---

```

vm.reversedMessage3='test'时,setter 会被调用


### 侦听器

虽然计算属性在大多数情况下更合适，但有时也需要一个自定义的侦听器。这就是为什么 Vue 通过 watch 选项提供了一个更通用的方法，来响应数据的变化。当需要在数据变化时执行异步或开销较大的操作时，这个方式是最有用的。

例如：

```html
<div id="watch-example">
    <p>
        Ask a yes/no question:
        <input type="text" v-model='question'>
    </p>
    <p>{{answer}}</p>
</div>
<script>

var timer = null;

var vm = new Vue({
    el: '#watch-example',
    data: {
        question: '',
        answer: 'I cannot give you an answer until you ask a question!'
    },
    watch: {
        question: function (newQuestion, oldQuestion) {
            this.answer = 'Waiting for you to stop typing...';
            this.getAnswer();
        }
    },
    methods: {
        getAnswer: function () {
            if (timer) {
                clearTimeout(timer);
            }
            timer = setTimeout(() => {
                console.log(vm.question)
            }, 500);
        }
    }
});

</script>
```

在这个示例中，使用 watch 选项允许我们执行异步操作 (访问一个 API)，利用函数防抖，最终得到想要的结果

## Class与Style绑定

操作元素的 class 列表和内联样式是数据绑定的一个常见需求。因为它们都是属性，所以我们可以用 v-bind 处理它们：只需要通过表达式计算出字符串结果即可。不过，字符串拼接麻烦且易错。因此，在将 v-bind 用于 class 和 style 时，Vue.js 做了专门的增强。表达式结果的类型除了字符串之外，还可以是对象或数组。

### 对象用法

我们可以传给 v-bind:class 一个对象，以动态地切换 class：

```html
<div id="app">
    <div class="static" v-bind:class='{"active":isActive,"text-danger":hasError}'></div>
    <div class="static" v-bind:class='classObject'></div>
    <div class="static" v-bind:class='classObject1'></div>
<script>
    var vm = new Vue({
        el: '#app',
        data: {
            classObject: {
                'active': true,
                'text-danger': true
            },
            isActive: true,
            hasError: true
        },
        computed: {
            classObject1: function () {
                return {
                    active: true,
                    'text-danger': true
                }
            }
        }
    })
    
    输出结果>>

    <div class="static active text-danger"></div>
    <div class="static active text-danger"></div>
    <div class="static active text-danger"></div>
</script>


```

### 数组用法

我们可以把一个数组传给 v-bind:class，以应用一个 class 列表：

```html
<div id="app">
    <div v-bind:class='[activeClass,errorClass]'></div>

</div>

<script>
    var vm = new Vue({
        el: '#app',
        data: {
            activeClass: 'active',
            errorClass: 'text-danger'
        }
    });
    
    输出结果>>
    <div class="active text-danger"></div>
</script>

```



### 用在组件上

当在一个自定义组件上使用 class 属性时，这些 class 将被添加到该组件的根元素上面。这个元素上已经存在的 class 不会被覆盖。

```html

<my-component class="baz boo"></my-component>

Vue.component('my-component', {
  template: '<p class="foo bar">Hi</p>'
})

结果>>
<p class="foo bar baz boo">Hi</p>

```

### 绑定内联样式

1. 对象语法


```html

<div v-bind:style="{ color: activeColor, fontSize: fontSize + 'px' }"></div>

data: {
  activeColor: 'red',
  fontSize: 30
}

```

直接绑定到一个样式对象通常更好，这会让模板更清晰：

```html
<div v-bind:style="styleObject"></div>

data: {
  styleObject: {
    color: 'red',
    fontSize: '13px'
  }
}

```

同样的，对象语法常常结合返回对象的计算属性使用。

2. 数组语法

```html

<div v-bind:style="[baseStyles, overridingStyles]"></div>

```

3. 自动添加前缀

当 v-bind:style 使用需要添加浏览器引擎前缀的 CSS 属性时，如 transform，Vue.js 会自动侦测并添加相应的前缀。

4. 多重值

从 2.3.0 起你可以为 style 绑定中的属性提供一个包含多个值的数组，常用于提供多个带前缀的值，例如：

```html

<div :style="{ display: ['-webkit-box', '-ms-flexbox', 'flex'] }"></div>

```