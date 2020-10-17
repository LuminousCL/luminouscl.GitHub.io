---
title:  Sort题型总结
tags:
  - 算法
---

### 写在前面

Android 中有几个比较有名的图片加载框架，Universal ImageLoader、Picasso、Glide和Fresco。它们各有优点，以前一直用的是ImageLoader 做项目中的图片加载，由于作者宣布ImageLoader 不会在更新了，因此新的项目打算换一个图片加载框架－Picasso, Picasso 是Square 公司开源的Android 端的图片加载和缓存框架。Square 真是一家良心公司啊，为我们Android开发者贡献了很多优秀的开源项目有木有！像什么Rerefoit 、OkHttp、LeakCanary、Picasso等等都是非常火的开源项目。扯远了，回到正题，除了使用简单方便，Picasso还能自动帮我们做以下事情：

- 处理Adapter 中ImageView的回收和取消下载。
- 使用最小的内存 来做复杂的图片变换。比如高斯模糊，圆角、圆形等处理。
- 自动帮我们缓存图片。内存和磁盘缓存。

以上只是列出了Picasso 比较核心的几点，其实它的优点远远不止这些，接下来就看一下如何使用Picasso。

![img](https://upload-images.jianshu.io/upload_images/3513995-26770e184b217649.png?imageMogr2/auto-orient/strip|imageView2/2/w/800/format/webp)

Picasso-Android.png

### 本文目录