---
title: JavaScript-Vue基础知识
date: 2020-09-25 19:40:28
tags: 
- Vue 
categories: JavaScript 
---

# 课程说明

1. **前置知识**

   ``html+css``、``JavaScript``

3. **两种学习路径**

   1. 稳扎稳打
      <img src="/images/image-20200512110024205.png" alt="image-20200512110024205" style="zoom:50%;" />

   2. 先用起来，再理解

      <img src="/images/image-20200512110824099.png" alt="image-20200512110824099" style="zoom:50%;" />

我们已第二种为例

# Vue开发体验

> vue官网地址：https://cn.vuejs.org/

1. **什么是vue？**

   vue是一个前端开发框架，用于降低UI复杂度

   UI: user interface 用户界面

2. **vue的特点**

   - 渐进式
   - 响应式
   - 组件化

# Vue核心概念

## Vue实例

通过`new Vue({...})`创建的对象

配置对象中的部分内容会被提取到vue实例中：

- data
- props
- methods
- computed


## 挂载

让vue实例控制网页中某个区域的过程，称之为挂载

挂载的方式：

1. 通过`el:"css选择器"`进行配置
2. 通过`vue实例.$mount("css选择器")`进行配置


## 模板

被vue实例控制的页面片段

1. **模板的作用是什么？**

   **为了提高渲染效率**，vue会把模板编译成为虚拟DOM树（VNode），然后再生成真实的DOM
    
   <img src="/images/image-20200512140602250.png" alt="image-20200512140602250" style="zoom:50%;" />
2. **模板书写到哪？**
   
   1. 在挂载的元素内部直接书写
   2. 在`template`配置中书写
   3. 在`render`配置中用函数创建

3. **模板中写什么？**

   1. 静态内容
   2. 插值：`{{JS表达式}}`，`mustache`语法
   3. 指令
      1. `v-html`：绑定元素的`innerHTML`
      2. `v-bind:属性名`：绑定属性
      3. `v-on:事件名`：绑定事件
      4. `v-if`：判断元素是否需要渲染
      5. `v-show`：判断元素是否应该显示
      6. `v-for`：用于循环生成元素
      7. `v-bind:key`：用于帮助在重新渲染时元素的比对，通常和`v-for`配合使用，以提高渲染效率
      8. `v-model`：语法糖，用于实现双向绑定，实际上，是自动绑定了value属性值，和注册了`input`事件
4. **模板中的代码环境**
5. 
   模板中所有的JS代码，它的环境均为`vue实例`，例如`{{title}}`，得到的结果相当于是`vue实例.title`

## 配置对象

1. `data`：数据
2. `template`：字符串，配置模板
3. `el`：配置挂载的区域
4. `methods`：配置方法
5. `computed`：配置计算属性

计算属性和方法的区别：

1. 计算属性使用时，是当成属性使用，而方法是需要调用的
2. 计算属性会进行缓存，如果依赖不变，则直接使用缓存结果，不会重新计算
3. 计算属性可以当成属性赋值
