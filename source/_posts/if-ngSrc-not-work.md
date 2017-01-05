---
title: ng-src图片加载失败怎么办
date: 2017-01-05 18:55:33
categories:
tags: [angular]

---

在Angular中，加载图片的方法是使用`ng-src`标签，如：
```html
<img ng-src="{{imgUrl}}"/>
```
其中`imgUrl`为图片地址，如果图片正常能显示，那这么使用一点问题没有，但是，如果图片加载失败了（例如该图片已经不存在，从而出现404错误），在该放图片的地方就会出现一个难看的图片加载失败图标，如果想把这个图标换成你自定义的图片，可以如下这么做：
**一、自定义指令（推荐）**
**HTML:**
```html
<img ng-src="{{imgUrl}}" err-src="{{errUrl}}"/>
```
**JavaScript:**
```javascript
var app = angular.module("MyApp", []);

app.directive('errSrc', function() {
  return {
    link: function(scope, element, attrs) {
      element.bind('error', function() {
        if (attrs.src != attrs.errSrc) {
          attrs.$set(‘src‘, attrs.errSrc);
        }
      });
    }
  }
});
```
这样一来，就把错误图标换成了你自己指定的地址`errUrl`，前提是`errUrl`这个图片是存在的。

**二、使用onerror属性**
```html
<img ng-src="{{imgUrl}}" onerror="this.src='/img/404.png'" />
```
使用这个方法，只适用于固定地址的图片，不能使用ng-bind的形式。

## 参考：
> [AngularJS中如果ng-src 图片加载失败怎么办](http://www.mamicode.com/info-detail-653185.html)