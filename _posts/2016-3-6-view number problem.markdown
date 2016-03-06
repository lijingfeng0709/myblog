---
layout: post
title:  "博客首页显示日志浏览量问题"
date:   2016-3-6 11:07:11 +0800
categories: html page
---
最近一直在鼓捣如何显示博客浏览量问题，于前天刚好看到一篇日志[《为你的博客添加访问量统计》](http://jerryzou.com/posts/introduction-to-hit-kounter/)。作者详细介绍了如何使用该插件，但笔者在使用过程中出现了难题，索性花费一整天解决了。

当我们想显示当前页面的访问量时，用`<span data-hk-page="current"> - </span>`。
显示指定页面时，更改data-hk-page的属性。笔者为了在日志列表中分别显示每个页面的浏览量时，对博客首页添加了如下代码
`<span data-hk-page="{ post.url | prepend: site.url }" style="padding-left:5px;padding-right:5px;"></span>`,
这段代码中` post.url | prepend: site.url `代表每片日志的地址，但是在显示过程中却显示浏览次数为0。如下图所示：
<div align="center"><img src="{{ site.baseurl }}/img/2016-3-6/1.jpg" /></div>
最后解析代码，发现网页该部分源码显示为：`<span data-hk-page="http://yourdomain.com/2016/01/01/test/" style="padding-left:5px;padding-right:5px;">10</span>`
出现这种原因，是因为在配置_config.yml文件中，我们未对url进行更改，把`url: "http://yourdomain.com" # the base hostname & protocol for your site`更改为你的博客地址，
比如我自己的更改为`url: "http://blog.lijingfeng.com" # the base hostname & protocol for your site`问题得以解决，效果图如下:
<div align="center"><img src="{{ site.baseurl }}/img/2016-3-6/2.jpg" /></div>

<h2>总结:</h2>

1、使用jekyll模版搭建博客时，多看看配置文件，尽量了解其功能，有哪些是需要自己配置的；

2、并且在调试代码的过程中，出了在本地上调试外，也需要在服务器上调试，找出问题根结所在。