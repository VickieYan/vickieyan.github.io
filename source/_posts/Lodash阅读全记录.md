---
title: 夕顔 | Lodash阅读全记录
date: 2018-07-27 10:46:30
tags:
---

在Jason哥的安利下成功入了Lodash的坑，刚看到这个单词的时候还在想为什么我问Jason哥避免重复提交怎么做他却给我安利一个懒加载的库😂，在github上查了一波才发现原来这是我们每天写的utils的集合版。

这篇文就用来记录一下阅读过程中的一些理解。



# 使用指南

## 安装

```shell
yarn add lodash
```

```javascript
import lodash from 'lodash'

window._ = loadash
```

# 方法解读

## isArrayLike

**用法**

```javascript
_.isArrayLike([1, 2, 3]);
// => true
 
_.isArrayLike(document.body.children);
// => true
 
_.isArrayLike('abc');
// => true
 
_.isArrayLike(_.noop);
// => false
```

**源码**

```javascript
const MAX_SAFE_INTEGER = 9007199254740991

function isArrayLike() {
    return value !== null && typeof value !== 'function' && isLength(value.length)
}

function isLength(value) {
    return 
    	typeof value === 'number' && 
        value > -1 && 
        value % 1 === 0 &&
        value <= MAX_SAFE_INTEGER
}
```

**源码解读**

判断一个数组是否是类数组的方法就是判断它是否有有效的length属性。





