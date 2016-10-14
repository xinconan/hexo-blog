---
title: typeerror-cannot-read-property-insertbefore-of-null
date: 2016-10-14 14:28:43
categories:
tags: angular
---
这两天在使用`angular`进行开发的时候，出现了如下错误：
```JavaScript
TypeError: Cannot read property 'insertBefore' of null
```
在网上找了一些资料，总结了下，需要在`ng-repeat`、`ng-if`等标签外面再加个`div`标签，
加上了就没有报错。  
错误前：
```html
<div ng-if="view.type !== 'ali'">
    <div>其他内容</div>
</div>
```
修改后：
```html
<div>
    <div ng-if="view.type !== 'ali'">
        <div>其他内容</div>
    </div>
</div>
```