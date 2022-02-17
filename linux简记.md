---
title: linux笔记 #文章页面上的显示名称，一般是中文
date: 2018-07-05 15:30:16 #文章生成时间，一般不改，当然也可以任意修改
categories: linux,笔记 #分类
tags: [linux,笔记] #文章标签，可空，多标签请用格式，注意:后面有个空格
description: linux命令这么多我该怎么记-如何查找Linux的命令
---

**linux命令这么多我该怎么记-如何查找Linux的命令**
https://linux.cn/lfs/LFS-BOOK-7.7-systemd/index.html

*find        查找*
> -name         名称
  -maxdepth     递归层级(大)  
  -mindepth     递归层级(小)  
  -user         用户  
  -group        属组  
  -perm         权限  
  -not          非(-not -user [name] #不是name用户,group等也可以组合)  
  -exec         后接要执行的命令(-exec chmod o-w # 根据查找到的文件将其他人的权限改为不可写)  

    free -m     查看内存的使用
    uname -a    查看内核版本
    locate      简单的查找文件
    ldd 	查看命令依赖
    whereis     程序名搜索-b二进制文件-m man说明文件 -s源代码文件
    which       搜索命令位置
    nl          查看文件内容会显示行号
    wc          统计文件信息
    type        查看是不是shell自带命令
    history     查看最近的所有命令可以陪grep使用，效果更好
    whoami      查看当前用户
    useradd     创建用户
    chmod       权限操作
    chown       修改文件所有者(属主)
    alias       取别名
    df -h       显示已经挂载的分区列表
    du -sh      查看目录占用空间
    du -h       查看文件大小
    sed 's/stringa1/stringa2/g' example.txt 替换命令，将example.txt文件中的 "string1" 替换成 "string2"
    dump -0aj -f /tmp/home0.bak /home 制作一个 '/home' 目录的完整备份
    nohup       使用nohup在登出ssh会话后仍继续运行命令
    ranger      文件浏览
    lsblk	查看磁盘挂载

**进程管理**

    kill pid    杀掉进程

**暂停并在后台运行命令**

    ctrl + z    暂停应用程序
    bg          让其在后台运行
    fg          重新将运用程序唤到前台

**linux命令行快捷键**

    ctrl + u    剪切光标前的内容
    ctrl + k    剪切光标至行未的内容
    crrl + y    粘帖
    ctrl + e    移动光标至行抹
    ctrl + a    移动光标到行首
    alt  + f    跳到下一个空格
    alt  + b    跳到上一个空格
    alt  + Backspace  删除前一个单词
    ctrl + w    剪切光标前一个单词
    ctrl + l    清屏
    stty + a    打印或查看控制字符(ctrl-c, ctrl-d, ctrl-z等)
    ^a^b^       替换上一个命令a变成b(命令输错可用)

**命令复用**

    !!          重复上一条命令
    c         重复上一条以ec开头的命令
    !76         用命令历史(history)中的76号命令

**{}()语法**

    touch name{1..10}.text
    $(cmd)  #执行cmd在替换原来的命令
    ()  # 命令组括号中的命令会在开一个子shell执行

