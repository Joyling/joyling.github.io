---
layout: post
title: Jekyll+github建站教程
categories:
- 工具
tags:
- github
- jekyll
---

> 作者做前端一年了，但是还没用过博客，东西一直写在云笔记上。现在发现博客是一个分享和学习的好方法，所以在windows上用jekyll和github搭建了一个简单的个人博客。

###一、注意事项

作者使用的操作系统是window7(64bit)

###二、注册github并搭建Page

1. [注册github](https://github.com/)
2. 新建一个REPOSITORY仓库名
3. **一定**是username.github.io（username为你的github用户名）
4. 进入项目，点settings
5. 点击automatic page generator(页面自动生成器)
6. 选择模板，现在已经可以访问username.github.io访问了


###三、本地安装jekyll

[jekyll](http://jekyll.bootcss.com/)是一个简单的免费的Blog生成工具,是一个静态站点生成器,它会根据网页源码生成静态文件。

它提供了模板、变量、插件等功能,所以实际上可以用来编写整个网站。


**Install Ruby**

1. [下载地址](http://rubyinstaller.org/downloads/ "ruby下载地址")
2. 安装

![](http://i.imgur.com/zl1vkDI.png)

3.通过ruby -v 来查看ruby是否正确安装

![](http://i.imgur.com/YuVq2DU.png)

4.如果出现了版本号，就代表安装正确


**Install DevKit**

1. [下载地址]( http://rubyinstaller.org/downloads/)
2. 点击下载文件进行解压
3. 安装

cd C:\rubydevkit            /*rubydevkit是安装路径*/

ruby dk.rb init				/*生成config.yml文件*/

ruby dk.rb install          

**修改gem镜像到taobao网**

gem -v  /*查看gem版本号，出现版本号说明gem安装正确*/

gem source --remove https://rubygems.org/

gem source -a https://ruby.taobao.org/

gem source /*查看gem的source是否为淘宝镜像*/

gem update --system

**安装jekyll**

gem install jekyll

**启动jekyll**

jekyll new myblog     /*创建一个kekyll文件，文件夹的名字是myblog*/

cd myblog            /*转到myblog目录下*/

jekyll serve         /*启动服务*/


**本地调试**

http://localhost:4000

###三、使用jekyll模板

**使用jekyll模板**

github有很多jekyll模板，fork下来，然后clone到本地，将模板文件拷贝到之前的myblog目录下。



**将myblog文件里的东西push到username.github.io仓库里**

###用markdown写下你第一篇blog吧
[markdown简介](http://www.jianshu.com/p/1e402922ee32/)

**MarkdownPad2注册码**

邮箱地址：Soar360@live.com

授权秘钥： GBPduHjWfJU1mZqcPM3BikjYKF6xKhlKIys3i

1MU2eJHqWGImDHzWdD6xhMNLGVpbP2M5SN6bnxn2kSE8qHq

NY5QaaRxmO3YSMHxlv2EYpjdwLcPwfeTG7kUdnhKE0vVy4R

idP6Y2wZ0q74f47fzsZo45JE2hfQBFi2O9Jldjp1mW8HUpTt

LA2a5/sQytXJUQl/QKO0jUQY4pa5CCx20sV1ClOTZtAGngSOJ

tIOFXK599sBr5aIEFyH0K7H4BoNMiiDMnxt1rD8Vb/ikJdhGM

MQr0R4B+L3nWU97eaVPTRKfWGDE8/eAgKzpGwrQQoDh+nzX1xo

VQ8NAuH+s4UcSeQ==


