---
title: Android Studio中Button等控件的Text中字符串默认大写的解决方法
date: 2016-08-10 06:01:22
categories:
- Android
tags: 
---
在Android Studio中xml里面添加一个Button、EditText等控件后，它的Text总是会显示大写，即使你输入的字符串是小写也不行，控制字符串大小写的属性  
```
android:textAllCaps
```
**解决办法**  

1.在你的控件中加入一条属性，这种方法只针对单个控件  
```
android:textAllCaps="false"
```
2.如果想所有控件都不自动大写，可以在res文件夹下的style.xml文件中添加  
```xml
<item name="android:textAllCaps">false</item>
```