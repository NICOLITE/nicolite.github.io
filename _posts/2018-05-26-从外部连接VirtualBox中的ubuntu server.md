---
title: 从外部连接VirtualBox中的ubuntu server
date: 2018-05-26 12:19:30
categories:
- Linux
tags:
- Linux
- Ubuntu
---
最近临近Java ee考试了，对于一直没上过课，也没看过书的渣渣来说，决定临时抱下佛脚。这时候就有个问题发生了，Windows上使用mysql简直是噩梦，装双系统又不值得，在虚拟机里面装个linux桌面发行版有点大材小用。这时候想到了一个比较理想的方法，那就是在VirtualBox中安装一个Ubuntu server，将mysql安装在上面，然后从外部连接使用。  

#### 首先在virtualbox中安装好ubuntu server

#### 然后打开virtualbox的设置，找到这里，连接方式选网络地址转换
![](https://raw.githubusercontent.com/nicolite/nicolite.github.io/master/images/20180526 -121930-1.png)  
#### 点击上图的端口设置，图中是我已经设置好的配置
![](https://raw.githubusercontent.com/nicolite/nicolite.github.io/master/images/20180526 -121930-2.png)  
#### 通过ifconfig命令可以知道子系统IP地址，对应上图中的子系统IP
![](https://raw.githubusercontent.com/nicolite/nicolite.github.io/master/images/20180526 -121930-3.png)
