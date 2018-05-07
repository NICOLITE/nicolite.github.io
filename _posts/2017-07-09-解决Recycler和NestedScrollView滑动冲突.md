---
title: 解决Recycler和NestedScrollView滑动冲突
date: 2017-07-09 07:28:33
categories:
- Android
tags: 
---
今天在项目中使用了多个RecyclerView，外层一开始使用了ScrollView，但是在屏幕外面的RecyclerView会折叠起来，撑不开 ，而且滑动不流畅，然后尝试了一下NestedScrollView，RecyclerView是撑开了，但是滑动问题依然在，通过查阅，找到了解决的方法，只需要在代码中调用recyclerView..setNestedScrollingEnabled(false)即可解决