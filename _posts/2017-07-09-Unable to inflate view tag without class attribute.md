---
title: Unable to inflate view tag without class attribute
date: 2017-07-09 07:04:14
categories:
- Android
tags: 
---
今天在做UI的时候出现了<span style="color: red;">Unable to inflate view tag without class attribute</span>在这个错误，编译部署到手机上时会崩溃出现<span style="color: red;">Attempt to invoke virtual method 'boolean java.lang.String.equals(java.lang.Object)' on a null object reference</span>

经过查找发现这是因为我在xml布局中使用了下面的空间来做分割线
```xml
 <view
                android:layout_width="match_parent"
                android:layout_height="0.5dp"
                android:background="@color/black"/>
```
只需要改为
```xml
<View
                android:layout_width="match_parent"
                android:layout_height="0.5dp"
                android:background="@color/black"/>
```