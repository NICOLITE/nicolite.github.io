---
title: You must not call setTag() on a view Glide is targeting
date: 2017-08-06 02:05:32
categories:
- Android
tags: 
---
##参考
[Glide加载图片报错You must not call setTag() on a view Glide is targeting](http://www.cnblogs.com/zzq-include/p/6135312.html)  
[You must not call setTag() on a view Glide is targeting的解决方案](http://blog.csdn.net/qq_26411333/article/details/52034444)
##起因
今天将项目中的Picasso换成Glide结果在一个RecyclerView的Adapter中出现了这个错误。
##原因
原因就是View使用setTag后导致Glide之前请求的标记被清除，强制转换过程中不能将你给定的类型判断为Request类型所致。
Glide为了防止加载图片错乱已经给图片打上标记了。
```java
@Override
public Request getRequest() {
Object tag = getTag();
Request request = null;
if (tag != null) {
if (tag instanceof Request) {
request = (Request) tag;
  } else {
throw new IllegalArgumentException("You must not call setTag() on a view Glide is targeting");
  }
 }
  return request;
 }
```
##解决方法
最直接的方法就是将删掉前面设置的setTag()，我就是这样解决的。  
更多方案参考[You must not call setTag() on a view Glide is targeting的解决方案](http://blog.csdn.net/qq_26411333/article/details/52034444)