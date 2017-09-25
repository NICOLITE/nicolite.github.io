---
title:  java.lang.IllegalStateException: You need to use a Theme.AppCompat theme (or descendant) with this activity.
date: 2017-03-15 12:39:12
categories:
- Android
tags: 
---
##错误

```
java.lang.IllegalStateException: You need to use a Theme.AppCompat theme (or descendant) with this activity.
```
##原因
这是因为活动中继承的是AppCompatActivity，但是你使用了Activity的主题。  
**解决方法**  
 1.将活动改为继承Activity  
 2.改为Theme.AppCompat主题

##注意
Activity的主题文件是在@android:style/Theme中
AppCompatActivity的主题在style/Theme.AppCompat中