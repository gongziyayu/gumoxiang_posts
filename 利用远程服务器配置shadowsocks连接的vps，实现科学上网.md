---
title: 利用远程服务器配置shadowsocks连接的vps，实现科学上网
date: 2017-07-18 23:26:07
toc: true
tags: 
  - vps
  - shadowsocks
  -  putty
---

　　自从买了域名和服务器之后，就开始了时不时地折腾，当然第一个折腾就是想着配置一个自己的vps来实现“科学上网”。本篇文章就来介绍下如何利用远程服务器配置shadowsocks连接的vps，实现科学上网。 (当然如何买域名和服务器的方法我就不赘述了，不懂或者遇到困难的朋友可以自行网上搜索，或者点击本站联系方式与博主一起探讨。)

## 使用第三方工具putty远程控制服务器

　　首先下载工具putty。(<a href="http://download.csdn.net/detail/gongziyayu/9800346">点我下载</a>)
  　　接着打开putty，配置如下图示： 
    ![](http://otan6vlz9.bkt.clouddn.com/putty.png)
　　
　　然后即可输入用户，密码进入vps控制界面了![](http://otan6vlz9.bkt.clouddn.com/puttycaozuovps.png)
## 在putty控制界面输入命令建立shadowsocks链接
 
　　在以上输入以下命令行并执行
```
1、 wget --no-check-certificate https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocks.sh
2、 chmod +x shadowsocks.sh
3、 ./shadowsocks.sh 2>&1 | tee shadowsocks.log
```
　　紧接着会让你输入shadowsocks的**端口密码等，输入后要记住，之后用客户端链接有用**
## 下载客户端Shadowsocks-win-2.5.6工具来链接配好的服务器

　　下载客户端Shadowsocks-win-2.5.6。（网上一搜就有很多的）
　　然后IP填写服务器的IP，密码端口填上步骤二里填写的密码端口，系统代理模式选择PAC模式即可。
  
