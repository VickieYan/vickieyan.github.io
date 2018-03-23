---
title: 夕顔 | 滚蛋吧！BUG君
date: 2018-03-23 17:14:03
tags:
---

事情是这样的。截取一个代码片段。

```html
<style>
    p { width: 10px; }
</style>

<p>1111111111111111111111111111111</p>
```

写组件的时候随手写了这么一段给卡片的文本部分占位，结果惊奇的发现文本竟然不换行！

按道理平时在 div 里插入文本如果限制了宽度会自动换行的。

于是我开始怀疑人生，难道我之前写的都是假代码，还是我有个假脑子。

于是我去搜了下文本如何换行。

```css
word-wrap: break-word;
```

我在根元素上加上这条属性过后，它确实换行了。

可是宝宝很倔强，宝宝不信，宝宝以前明明不加它也换行的。

正在百思不得其解之时，Jason 哥屁颠屁颠跑过来说：「只有中文才会自动换行。」

于是亲测一波，结果如下：

```html
<!--不换行-->
<p>1234567890</p>
<!--换行-->
<p>1 2 3 4 5 6 7 8 9 0</p>
<!--不换行-->
<p>I'malonglonglonglonglonglonglongtext.</p>
<!--换行-->
<p>I'm a long long long long long long long text.</p>
<!--换行-->
<p>我是超级长长长长长长长文本</p>
```

所以说，默认情况下中文是自带换行属性的，而非中文的情况下有空格才会自动换行。

这里顺便测试了一波其他几个换行属性。

* [word-break: break-all] : 相当于把单词全部击碎，可具有和中文一致效果，对英文和数字均生效。
* [word-wrap:break-word] : 效果和上述类似，但是略有区别，如果一行容纳不下该单词时会自动换行，下面附图解释。
  ![img](http://m.qpic.cn/psb?/V10ZHE9M4DB6nN/a*Xv46*psumtR3TsnBlJcSYqTsXgbxUrkoQ*TFSpXOA!/b/dEMBAAAAAAAA&bo=HQHPAR0BzwEDByI!&rf=viewer_4)
* [white-space:nowrap] : 强制不换行，对所有元素都生效。
* [text-overflow: ellipsis] : 溢出部分转换为省略号。顺带一提，这个属性只对水平方向溢出生效。垂直方向的解决方案如下(部分浏览器支持)。

```css
div {
  display: block;
  width: 300px;
  text-overflow: ellipsis;
  overflow: hidden;
  max-height: 200px;
  display: -webkit-box;
  -webkit-line-clamp: 7;
  -webkit-box-orient: vertical;
}
```
