---
title: javascript自定义方法封装
date: 2019-09-30 10:00:27
tags: 
- JavaScript 
categories: JavaScript 
description: 常用方法的封装以及javascript内部方法的实现
---

# 实现dom的获取

不用document.getElementXXXX方法来获取
.w 类名为w的元素
#w id为w的元素
div 标签为div的元素


```javascript
/**
 * 根据指定的选择器获取dom元素集合
 * @param {String} selector 选择器 如.className、#divName、div 
 * @param {Document[]} list 获取到的dom元素集合
 */
function getDom(selector = '', list = []) {

    /**
     * 获取对应元素选择器以及选择器名称,如{type:"id",value:"className"}
     */
    function getType() {
        var classReg = /^\.\w+/;
        //类选择器正则
        var idReg = /^\#\w+/;
        //id选择器正则
        if (classReg.test(selector)) {
            return {
                type: 'class',
                value: selector.slice(1)
            }
        } else if (idReg.test(selector)) {
            return {
                type: 'id',
                value: selector.slice(1)
            }
        } else {
            return {
                type: 'tag',
                value: selector.toUpperCase()
            }
        }
    }
    /**
     * 获取属性值
     * @param {Document} ele 
     * @param {String} type 
     */
    function getAttr(ele, type) {
        return ele.getAttribute(type) || "";
    }

    /**
     * 
     * @param {Document} ele dom元素 
     * @param {Document[]} list 获取到dom元素数组
     * @param {*} type 选择器类型 
     * @param {*} value 对应获取选择器的值
     */
    function treeTravelsal(ele, list, type, value) {
        if (getAttr(ele, type).split(' ').indexOf(value) !== -1) {
            list.push(ele);
        }
        if (ele.tagName === value && type === 'tag') {
            list.push(ele);
        }
        var len = ele.children.length || 0;
        for (var i = 0; i < len; i++) {
            treeTravelsal(ele.children[i], list, type, value);
        }
    }

    var obj = getType(selector);
    treeTravelsal(document.body, list, obj.type, obj.value);
    return list;
}
```


