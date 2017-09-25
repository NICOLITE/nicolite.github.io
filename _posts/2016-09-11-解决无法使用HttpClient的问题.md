---
title: 解决无法使用HttpClient的问题
date: 2016-09-11 12:57:17
categories:
- Android
tags: 
---
在android M（6.0）中谷歌将Apache HttpClient移除了，但也并不是完全删除。不过以后还是尽量避免使用，毕竟谷歌已经抛弃了  
**解决方法**  
1、对于用android studio的朋友，google官方就有解决方案，就是在 build.gradle 文件中加入以下代码，注意是Module:app那个文件  
```
android {
useLibrary ‘org.apache.http.legacy’
}
```
2、对于还在用eclipse的朋友，那就是把org.apache.http.legacy.jar这个包加入到项目的libs当中，这个jar包在\sdk\platforms\android-23\optional下面  