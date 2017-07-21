---
title: vps服务器上搭建hexo静态博客教程
date: 2017-07-21 23:27:17
toc : true
tags:
  - hexo
  - yilia
  - 静态博客

---
	   在博客搭建的路上我遇到过很多问题，由于网上资源驳杂，不同人的写作节奏不一样，经常导致写作的人懂，而读的人跟着操作得不到想要的东西，关键在于那点没有讲出的东西。 在此，我分享出自己查找及思考后得到的思路给大家，如还有不懂的或者不成功的，可以点击联系方式联系我，欢迎指教！（若小白想知道本地初始化hexo及域名购买服务器搭建等也可联系在下……）
		整体思路：首先安装好需要的工具，然后在vps的某个能访问的目录上新建文件夹，在文件夹里 使用hexo init初始化hexo环境。此处得出的都不需要动，只需要修改config文件去配置。  然后在github里fork你想要的主题，对就是这个主题将他clone到hexo初始化的 themes/(主题名)文件夹下。  此后一切修改主题的样式，功能等都在新建的(主题名)文件夹下修改，可以在本地修改好传到git，再操作vps服务器pull。 最后写文章的可以 在github里新建个资源，用来储存你要写的文章，最后clone到hexo根目录下的source/_post文件夹下。
        
<!-- more -->
 ##  debian系统安装 nginx  

 - 编辑 /etc/apt/sources.list ，添加以下两行。（Debian版本代号分别为5.0的 lenny，6.0的 squeeze ，7.0的 wheezy 和8.0的 jessie，至于还没发布的9.0则为 stretch，你只需要根据你使用的版本更换对应的版本代号即可，自己使用的版本可以在服务器上看，首先要先安上自带的nginx才能升级啊）
```
deb http://nginx.org/packages/debian/ 版本代号 nginx
deb-src http://nginx.org/packages/debian/ 版本代号 nginx
```
 - 更新并导入升级Key
```
wget http://nginx.org/keys/nginx_signing.key && apt-key add nginx_signing.key && apt-get update && apt-get install nginx
```
 ## debian系统安装node js 
  - 下载源码(去官网找到能用的最新的替掉node-v0.12.1.tar.gz)
```
wget http://nodejs.org/dist/node-v0.12.1.tar.gz
```
- 安装g++ （如果已经安装，可跳过）
```
 apt-get install g++
  apt-get install pkg-config  (必须，如果不执行有可能编译不通过)
```
  - 解压，安装
```
tar zxvf node-v0.4.9.tar.gz
  cd node-v0.4.9
  ./configure
  make 
  make install
```
  - 检验版本
```
node -v
```
 ##  git安装
```
apt-get install git
```
 ##  hexo模块安装
```
cd ~/hexo  ##此处打开的文件夹是你的博客要放的地方,hexo文件夹是自己新建的
npm install hexo-cli -g
npm install
//进入文件夹
hexo init
```
<font color="red">hexo初始化之后，使用的默认主题；可以使用 git clone xxx  theme/xx  将需要的主题下载到themes文件夹；写的文章放的地方同理，可参考整体思路。   以下是个操作小例子，可以略去不看</font>
```
git clone  https://github.com/gongziyayu/gumoxiang.git  theme/yilia
//以下为修改
git  pull  //取下
git  add *  //保存本地到储存区
git  status  //查看文件状态
git  commit -m "xxx"//提交
git push    //推送改动到github
```
 ## nginx的配置
  - 新建个配置文件
```
cd /etc/nginx/conf.d/
vi hexo.conf
```
  - 配置内容
```
server {
    listen          80;
    server_name     gumoxiang.com www.gumoxiang.com;  # 你的域名
    location /root{
        root         hexo;                            #就是要访问的根目录
        index        index.html;               ##默认的去找哪个文件
    }
}
```
  - 重新加载或启动
```
nginx -s reload
```
## 使用命令生成静态文件

  - 切换到你的博客目录，使用以下代码生成静态文件并编译，启动服务
```
hexo  g           #生成可访问文件在public文件夹里
hexo   d         #部署文件
hexo   s       #启动服务
```
  - 然后你访问localhost:4000(如果远程操作服务器,localhost就要换成服务器IP地址)，就看到你的博客的样子啦，如下图示：
  -![](http://otan6vlz9.bkt.clouddn.com/siteblog001.png)
 

	  好啦，到此基本的功能都完了。如果想加点别的功能或者优化，可以网搜或者等待下篇文章^_^
 
