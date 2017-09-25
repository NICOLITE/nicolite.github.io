---
title: Can't create handler inside thread that has not called Looper.prepare()
date: 2017-04-05 11:52:11
categories:
- Android
tags: 
---
**错误**
```
java.lang.RuntimeException: Can't create handler inside thread that has not called Looper.prepare()
```
****
在子线程创建了AlertDialog
**解决方法**
```java
runOnUiThread(new Runnable() {
                            @Override
                            public void run() {
                              //在这里new AlertDilog
                            }
  }
```