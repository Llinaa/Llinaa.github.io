---
title: whistle代理工具抓包
date: 2018-12-27 20:30:07
categories:
- 工具
tags:
- 工具
---
最近在做小程序开发，需要进行抓包，使用了whistle

1、安装浏览器代理插件SwitchyOmega
2、npm install -g whistle    
   启动：w2 start 
3、在SwitchyOmega中添加whistle
    ![Alt text](/assets/img/whistle.png)
4、手机连接wifi，与电脑同wifi网段。这样手机才能访问到PC，手机
  配置代理，此时就可以在whistle中抓到手机上的http包
5、抓https包，手机上需安装证书，
ios配置代理后，用Safari打开网址：http://rootca.pro，下载后安装
最后，设置----通用-----关于本机------证书信任设置------>找到whistle证书打开信任
安卓直接扫码安装  
    ![Alt text](/assets/img/andriod.png)
    
最后，进入要抓包的app就ok拉
    
