---
title: 如何获得linux源码
date: 2018-11-05 15:30:16 #文章生成时间，一般不改，当然也可以任意修改
categories: 日志
tags: [linux] #文章标签，可空，多标签请用格式，注意:后面有个空格
description: 如何获得linux源码
---

1.终端输入which [命令名],获取程序所在目录
2.输入dpkg -S [命令路径],得知命令所在包
3.sudo apt-get source [包名],下载指定的包
4.如果遇到找不到合适的源的问题请用root权限编辑/etc/apt/sources.list添加国内源,个人觉得网易的不错
5.下载源更新完毕后,就可以下载了,源码文件在包的src目录下
