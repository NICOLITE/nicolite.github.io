---
title: Android Studio Error:前言中不允许有内容。
date: 2017-02-13 18:59:50
categories:
- Android
tags: 
---
Error:(1, 1) Error: 前言中不允许有内容。

由Eclipse转向Android Studio 的新手，在引用assets 目录的时候，通常会习惯性的把assets文件新建在res目录下，这样做，在引用这个文件的时候通常会报这样的错：
```
Error:(1, 1) Error: 前言中不允许有内容。
```
出现这样的错误是你的程序在调用的时候，识别到assets目录的路径有误造成的，在Android Studio 中，assets 目录与res目录应该放在同一级目录下的。

所以解决方法比较简单：
把assets的文件移至src/main/目录下即可。

<img title="" src="http://img.blog.csdn.net/20161014110957276" alt="assets" />