---
title: Jascript数组扩展
date: 2019-09-24 17:39:32
tags: 
- JavaScript 
categories: JavaScript 
description: 数组方法的自定义实现
---

# foreach

数组的每个元素执行一次提供的函数。

```javascript
var person = [{ name: '王港', age: 18 },
{ name: '刘莹莹', age: 23 },
{ name: '王秀莹', age: 25 }];

person.forEach(function (ele, index, self) {
    //ele:数组每一项，index:数组索引，数组本身
    console.log(ele, index, self);
})

Array.prototype.myForEach = function (func) {
    //this指向调用者(数组)
    var _arr = this, len = this.length;
    for (var i = 0; i < len; i++) {
        //arguments[1]指向调用函数中dethis指向谁
        func.apply(arguments[1] || window, [_arr[i], i, _arr])
    }
}

person.myForEach(function (ele, index, self) {
    //this指向{"sex": '男'}
    console.log(ele, index, self, this)
}, { "sex": '男' })

```




# filter

创建一个新数组, 其包含通过所提供函数实现的测试的所有元素。

```javascript
var newArr = person.filter(function (ele, index, self) {
    console.log(this);
    return ele.age > 23;
}, { dom: 'dom' })
//此处的数组项 指向的还是同一块内存地址，改变一个另外一个也会修改 可通过克隆的方式创建没有关系的独立数组
newArr[0].name = '123'  
console.log(newArr);
console.log(person)

Array.prototype.myFilter = function (func) {
    var _arr = this, len = this.length, newArr = [];
    for (var i = 0; i < len; i++) {
        func.apply(arguments[1] || window, [_arr[i], i, _arr]) ? newArr.push(_arr[i]) : "";
    }
    return newArr;
}
```



# map

方法创建一个新数组，其结果是该数组中的每个元素都调用一个提供的函数后返回的结果。

```javascript

var newarr = person.map(function (ele, index, self) {
    console.log(ele, index, self, this);
    ele.age = ele.age * 2;
    return ele;
}, { dom: 'dom' })

//此处的数组 newarr还是指向person

Array.prototype.myMap = function (func) {
    var _arr = this, len = this.length, newarr = [];
    for (var i = 0; i < len; i++) {
        newarr.push(func.apply(arguments[1] || window, [_arr[i], i, _arr]))
    }
    return newarr;
}

```

# every

方法测试一个数组内的所有元素是否都能通过某个指定函数的测试。它返回一个布尔值。

```javascript

var b = person.every(function (ele, index, self) {
    console.log(ele, index, self, this);
    return ele.age > 23;
}, { dom: 'dom' })

Array.prototype.myEvery = function (func) {
    var _arr = this, len = this.length, flag = true;
    for (var i = 0; i < len; i++) {
        if (!func.apply(arguments[1] || window, [_arr[i], i, _arr])) {
            flag = false;
            break;
        }
    }
    return flag
}

```

# some

方法测试数组中是不是有元素通过了被提供的函数测试。它返回的是一个Boolean类型的值。

```javascript

var b = person.some(function (ele, index, self) {
    console.log(ele, index, self);
    return ele.age > 30
})

Array.prototype.mySome = function (func) {
    var _arr = this, len = this.length; flag = false;
    for (var i = 0; i < len; i++) {
        if (func.apply(arguments[1] || window, [_arr[i], i, this])) {
            flag = true;
            break;
        }
    }
    return flag
}

```

# reduce

方法对数组中的每个元素执行一个由您提供的reducer函数(从左向右执行))，将其结果汇总为单个返回值。

```javascript
var cookie = `BIDUPSID=FEFF6EF48A14D731758822E71EDAB720; 
                PSTM=1567387707; 
                BD_UPN=12314753; 
                BAIDUID=85C615F1F00B0D7631759024DBD84EF8:FG=1; 
                H_WISE_SIDS=135670_124610_136262_114552_135964_135926_128070_120173_135727_132911_131247_122159_132378_131517_118884_118866_118851_118818_118804_107315_133352_129654_136193_132250_124632_131861_128968_135307_135812_132551_135433_135873_134046_134751_131423_136164_135464_110085_134253_134154_127969_131755_131951_135624_135461_127416_135035_134652_132764_135834_136259_136076; 
                MCITY=-233%3A; BDORZ=B490B5EBF6F3CD402E515D22BCDA1598; 
                BD_HOME=1; 
                H_PS_PSSID=1432_21085_29523_29720_29568_29221_26350; 
                BDRCVFR[feWj1Vr5u3D]=I67x6TjHwwYf0; 
                delPer=0; 
                BD_CK_SAM=1; 
                PSINO=1; 
                sugstore=1`;

function parseCookie(str) {
    var obj = {}, arr = null;
    arr = str.split(';');
    arr.reduce(function (prev, icur, index, self) {
        var icurArr = icur.split('=');
        prev[icurArr[0]] = icurArr[1];
        return prev
    }, obj)
    return obj;
}

Array.prototype.myReduce = function (func) {
    var _arr = this, len = this.length, nextValue = arguments[1];
    for (var i = 0; i < len; i++) {
        nextValue = func.apply(arguments[2] || window, [nextValue, _arr[i], _arr])
    }
    return nextValue;
}

```


# reduceRight

方法对数组中的每个元素执行一个由您提供的reducer函数(从左向右执行))，将其结果汇总为单个返回值。

和reduce相反 参考reduce实现

# 数组算法题

1. 对于字符串"abc1234"变成4321cba

```javascript
//转换成数组--反转--在拼接字符串
var str='123abc';
console.log(str.split('').reverse().join(''))

```

2. 查找有序数组中的某向,并返回索引(二分查找(binary search))

```javascript

function binarySearch(arr, element) {
    var minIndex = 0;
    var maxIndex = arr.length - 1;
    var testElement;
    while (minIndex <= maxIndex) {
        var middleIndex = Math.floor((minIndex + maxIndex) / 2)        
        testElement = arr[middleIndex]
        //所要查找的值在右边
        if (testElement < element) {
            minIndex = middleIndex + 1;
        } else if (testElement > element) {
            maxIndex = middleIndex - 1;
        } else {
            return middleIndex;
        }
    }
    return -1;
}

```

3. 判断数组是否是对称数组（从左向右读和从右向左读，都是一致的，称为对称数组）

```javascript
//对称数组
function symmetryArr(arr) {
    var minIndex = 0;
    var maxIndex = arr.length - 1;
    while (minIndex <= maxIndex) {
        if (arr[minIndex++] !== arr[maxIndex--]) {
            return false;
        }
    }
    return true;
}

```

4. 查询字串首次出现的位置，如：原串abcbcxyxyz 字串为cx 结果为4

```javascript

var str = "abefbaxzbc";
var subStr = "c";

//indexOf 内部实现
function getIndex(str, subStr) {
    var subStrLen = subStr.length;
    var len = str.length - subStrLen;
    for (var i = 0; i <= len; i++) {
        for (var j = 0; j < subStrLen; j++) {
            if (subStr[j] != str[i + j]) {
                break;
            }
            if (j == subStrLen - 1) {
                return i;
            }
        }
    }
    return -1;
}

```

5. 计算数组中，最大连续增长子序列的长度，如[1,2,3,4,1,2,3,4,5,,1,2,3] 结果为5

```javascript

var arr = [1, 2, 3, 4, 5, 1, 2, 5, 6, 7, 10, 1, 3, 4, 13, 17, 22, 32, 50, 80];
function getMaxLength(arr) {
    var addNum = 1;
    var len = 0;
    for (var i = 1; i < arr.length; i++) {
        if (arr[i] > arr[i - 1]) {
            addNum++;
        } else {
            len = addNum > len ? addNum : len;
            addNum = 1;
        }
    }
    len = addNum > len ? addNum : len;
    return len;
}
console.log(getMaxLength(arr));


```
   

# 基础练习题

## web标准是什么

Web标准，使得Web开发更加容易。

简单来说web标准可以分为结构（html），表现（css）和行为（JavaScript）。

结构主要是有html标签组成，在页面body里面我们写入的标签都是为了页面的结构。 标准由万维网联盟(W3C)制定 https://www.w3.org/html/

表现即是css样式表。通过css可以让结构标签变得更具美感。 标准由万维网联盟(W3C)制定  https://www.w3.org/TR/CSS22/

行为指的是页面与用户具有一定的交互，主要是有js组成。标准由ECMA制定 https://www.ecma-international.org/

## 浏览器中body默认的margin

标准是8px,ie浏览器7及以下 上下15px左右10px

## 元素居中

1. 如果宽高都为auto的绝对定位元素,通过left和right可以调整其宽度
2. 如果宽高都为auto的绝对定位元素,通过top和bottom可以调整其高度

## typeof 返回的结果

"number"、"string"、"object"、"function"、"undefined"、"boolean"
