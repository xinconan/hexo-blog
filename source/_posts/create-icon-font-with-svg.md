---
title: 使用svg创建icon-font图标
date: 2017-03-29 19:43:02
categories:
tags: icon-font
---
在开发webapp时，经常会用到UI给的小图标，UI一般会提供png和svg两种格式。使用png经常需要考虑不同分辨率和dpr设备的差异，一个图标UI可能会提供两到三种不同大小的图片，这样处理很不方便。直接使用svg的话，svg单独一个文件会耗网络请求，嵌入到html中又会使html变得臃肿，重复利用率不高。使用icon-font可以直接使用class的方式，显示图标，而且和字体一样，可以设置大小和颜色，非常方便。

介绍一种可以直接将svg创建icon-font字体的网站，[https://icomoon.io/app](https://icomoon.io/app)，如下图所示，直接导入UI给的svg（最好提前用class的方式进行命名，方便后续使用）。
![icomoon.io](https://xinconan.oschina.io/blogimages/icomoon.png)
选择要导出的图标，点击“生成字体”按钮，在该页面可以预览要导出的字体图标及对应的编码。
![icomoon.io](https://xinconan.oschina.io/blogimages/icomoon_preview.png)
点击设置，可以设置字体的名称和class前缀，还可以生成对应的sass、stylus、less文件等。
![icomoon.io](https://xinconan.oschina.io/blogimages/icomoon_config.png)
点击“download”，就可以下载字体，然后进行使用啦。