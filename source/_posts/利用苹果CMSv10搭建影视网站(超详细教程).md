---
title: 利用苹果CMSv10搭建影视网站(超详细教程)
tags:
  - 建站
categories:
  - 教程
abbrlink: 1cc5eeae
date: 2020-07-02 14:23:30
index_img: https://gitee.com/Stubborner/images/raw/master/images/9bd9b167gy1g2qm1v14x0j21hc0u0e81.jpg
---

## 准备

- 一台服务器
- [苹果CMSv10 版本源码](http://www.maccms.cn/down.html)
<!--more-->
## 安装宝塔面板

[安装教程见宝塔官网](https://www.bt.cn/bbs/thread-19376-1-1.html)

安装完宝塔后，在软件商店里把运行环境安装了，网站运行环境有如下:

lamp 的全称是linux + apache + mysql +php
lnmp 的全称是linux + nginx + mysql + php 

看个人喜好安装就行

![](https://gitee.com/Stubborner/images/raw/master/images/lamp.png)

## 安装苹果CMSv10系统

1. 在宝塔中添加网站

   ![](https://gitee.com/Stubborner/images/raw/master/images/cite.png)

2. 将下载好的苹果cmsv10源码通过宝塔上传到服务器的www/wwwroot目录下并解压

   <img src="https://gitee.com/Stubborner/images/raw/master/images/yuanma.png" style="zoom:100%;" />

3. 浏览器访问服务器ip或域名(域名必须已经绑定了ip后出现苹果cms安装界面,点开始安装

   ![](https://gitee.com/Stubborner/images/raw/master/images/install.png)

4. 若出现以下界面请到宝塔面板为该站点php安装fileinfo模块(如还不能解决请更换php版本)

   ![](https://gitee.com/Stubborner/images/raw/master/images/sqlpeizhi.png)

   ![](https://gitee.com/Stubborner/images/raw/master/images/changephp.png)

5. 配置数据库信息

   ![](https://gitee.com/Stubborner/images/raw/master/images/cmsset.png)

6. 出现以下情况请到宝塔面板将该站点文件夹下的admin.php改名,并重新通过访问(ip/改名后的admin.php的文件名)进入cmsv10后台管理界面

   ![](https://gitee.com/Stubborner/images/raw/master/images/adminset.png)

7. 出现以下界面成功安装了cmsv10系统

   ![](https://gitee.com/Stubborner/images/raw/master/images/success.png)

## 为cms系统配置采集站

1. 百度电影采集站，并按该站点的帮助中心配置采集站

   ![](https://gitee.com/Stubborner/images/raw/master/images/mac10.png)

2. 这里以秒播采集站讲解，添加采集站接口先必须先添加对应的播放器,否则会出现无法播放的结果，操作完成后点击后台右上角[清缓存]，此时再看数据，已经可以正确的选择播放器并且可正常播放了

   ![](https://gitee.com/Stubborner/images/raw/master/images/caiJi.png)

3. 设置自动采集请参考采集站的帮助中心教程，讲的很详细，我就不多赘述了

4. 其他的配置根据个人情况配置即可