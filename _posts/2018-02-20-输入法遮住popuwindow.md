---
title: 输入法遮住popuwindow
date: 2018-02-20 21:59:33
categories:
- Android
tags: 
- Android
- popuwindow
---
做个记录，一直以来用的都是Android M的测试机，今天换了一台Android L的测试机，结果出现输入法将popuwindow输入框给遮住了，在Android M和Android N的机器上可是一切正常的，一开始以为是popuwindow的layout文件没有加fitsSystemWindows导致的，但是加上去后还是会遮住，显然不是这个问题。 

### 解决方法 

```java
popuWindow.setSoftInputMode(WindowManager.LayoutParams.SOFT_INPUT_ADJUST_RESIZE | WindowManager.LayoutParams.SOFT_INPUT_STATE_HIDDEN);
popuWindow.setInputMethodMode(PopupWindow.INPUT_METHOD_NEEDED);
```


### 参考

[输入法遮住PopupWindow中的EditText ](http://bbs.csdn.net/topics/391814331)