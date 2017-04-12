---
layout: post
title:  React Native Navigator
date:   2017-03-21 14:14:00
categories: ReactNative
tags: ReactNative
---
## 1、按照[官方](https://facebook.github.io/react-native/docs/integration-with-existing-apps.html)操作来

基本操作流程按照官网的来，主要有几个地方要注意一下：

1) 在给app/build.gradle添加react-native依赖的时候，要把那个加号改成你通过npm下载后的具体版本：

{% highlight %}
compile "com.facebook.react:react-native:0.43.3"
{% endhighlight %}

2) 在项目根目录build.gradle中指定react-native路径时要写对路径，这点尤其重要，否则的话android studio会
到maven center中去下载相应的react native依赖，导致各种不兼容和莫名其妙的错误！这个也是一开始没有把那个+
改成具体的版本造成的！

{% highlight %}
allprojects {
    repositories {
        maven {
            // All of React Native (JS, Android binaries) is installed from npm
            url "$rootDir/node_modules/react-native/android"
        }
        // ......
    }
}
{% endhighlight %}

3) 在执行npm install --save react react-native操作的时候，系统给出了如下警告：
npm WARN react-native@0.43.3 requires a peer of react@16.0.0-alpha.6 but none was installed
当时多此一举的又通过npm install react@16.0.0-alpha.6来安装了一下，导致后来也是各种模块找不到的问题，
所以，不要手贱了


## 2、项目运行中出现的问题

1) 记得加SYSTEM_ALERT_WINDOW权限

2) 在运行之前先要通过npm start启动服务，否则报could not get batchbridge错误


其他还有一些什么错误也忘记了，总之，如果按照官网的步骤来执行的话出现了各种莫名其妙的错误，
最好的办法就是把node_modules目录和package.json全部删除干净，然后重新来操作一遍！因为有些时候
可能因为网络还是什么原因，导致下载的模块可能出现问题。

