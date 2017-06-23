---
title: pxtorem在webpack中出现的问题
date: 2017-06-22 11:01:16
categories:
tags: 前端
---

最近在使用[antd-mobile](https://mobile.ant.design)开发新项目，使用了它提供的[高清方案](https://github.com/ant-design/ant-design-mobile/wiki/antd-mobile-0.8-%E4%BB%A5%E4%B8%8A%E7%89%88%E6%9C%AC%E3%80%8C%E9%AB%98%E6%B8%85%E3%80%8D%E6%96%B9%E6%A1%88%E8%AE%BE%E7%BD%AE)。按照其设计规范，开发过程中使用`px`为css单位，build根据`1rem=100px`(dpr=2)换算，所以用到了[postcss-pxtorem](https://github.com/cuth/postcss-pxtorem)。

以下是项目中webpack.config.js的主要配置：
```javascript
loaders: [
{
    test: /\.scss$/,
    loader: ExtractTextPlugin.extract('style-loader', 'css-loader?sourceMap!sass-loader!postcss')
 }],
postcss: [
    autoprefixer({browsers: ['last 5 versions']}),
    pxtorem({rootValue: 100, propWhiteList: []})
]
```
然后出现了个“诡异”的问题，正常的`.scss`文件中的`px`都正常转成`rem`了，但是当`scss`文件中import了其他的`scss`文件，引入的文件中的px不会被转成`rem`。当时认为是`pxtorem`插件的问题，还傻傻的去`pxtorem`的GitHub上提了个[issue](https://github.com/cuth/postcss-pxtorem/issues/38)。后面在[postcss-loader](https://github.com/postcss/postcss-loader)的文档上找到了问题：
> You can use it standalone or in conjunction with `css-loader` (recommended). Use it after `css-loader` and `style-loader`, but before other preprocessor loaders like e.g `sass|less|stylus-loader`, if you use any.

就是`postcss`要放到`sass-loader`之前执行，所以改成下面问题就解决了：
```javascript
{
    test: /\.scss$/,
    loader: ExtractTextPlugin.extract('style-loader', 'css-loader?sourceMap!postcss!sass-loader')
 }
 ```