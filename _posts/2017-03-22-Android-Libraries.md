---
layout: post
title:  Android Libraries
date:   2017-03-22 08:55:00
categories: Android
tags: Android
---
## [原文](http://mp.weixin.qq.com/s/-4yo1I8bKbRMvBdSd2kQcg)

## [Lottie](https://github.com/airbnb/lottie-android)


这是一个能解析 Adobe After Effects 动画导出的JSON文件并把它们渲染成本地动画的库。在Google Play Store 上有一个示例app。

github上超过7500颗星，应该不会错!

## [PreviewSeekBar](https://github.com/rubensousa/PreviewSeekBar)

如果你使用Google Play Movies，你可能注意到了这个动画效果很棒，可以预览电影的SeekBar。 Rúben Sousa 实现了这种效果并开源。下面的gif图片很好的说明了其功能。如果你的app是一个播放器，你决定应该试试

## [CoordinatorTabLayout](https://github.com/hugeterry/CoordinatorTabLayout)

CoordinatorTabLayout是一个自定义的组合控件，帮助你快速实现TabLayout与CoordinatorLayout相结合的样式。

## [excelPanel](https://github.com/zhouchaoyuan/excelPanel)

RecyclerView实现的二维表格，不仅可以加载历史数据，还能加载新数据

## [FlowLayout](https://github.com/hongyangAndroid/FlowLayout)

一个让子view在空间不够的情况下自动跳到下一行的布局。子view之间的间隔由 FlowLayout计算出来，以便让view是均匀分布的

## [CameraFragment](https://github.com/florent37/CameraFragment)
一个集成了拍照功能的Fragment ，根据README：

CameraFragment直接预览camera视图，并提供简单的API来捕获或者管理设备。你可以使用 CameraFragment 设置自己的布局以及控制camera

## [boxing](https://github.com/Bilibili/boxing)

Boxing是一个基于MVP模式的Android多媒体选择器，你可以：

图片选择(单/多选)，

预览或者剪裁图片。

它还支持gif，视图选择，图片压缩以及自定义UI


## [ObjectBox](https://github.com/greenrobot/ObjectBox)

greenrobot宣称：

性能是我们创建ObjectBox的首要因素。之前我们创建了安卓和 SQLite上 最快的对象关系映射 (ORM) greenDAO 。自从2011年第一个版本发布以来，我们对对象持久化-以及 SQLite的缺陷有了许多认识。我们意识到， 要显著提高移动端的性能，需要从核型开始，创建一个基于对象的数据库。

## [Store](https://github.com/NYTimes/Store)


Store是一个异步加载和缓存库。文档描述：

Store是一个简化数据的请求，解析，保存，以及数据重试的类。一个Store类似于 仓库模式 ，不过用 RxJava封装成了响应式的API，以支持单向数据流 。

文档非常易懂，这个库值得尝试。你可以尝试各种flows，比如数据请求，缓存，解析等