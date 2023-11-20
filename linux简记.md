---
title: linux笔记 #文章页面上的显示名称，一般是中文
date: 2023-11-03 11:0   #文章生成时间，一般不改，当然也可以任意修改
categories: linux,笔记 #分类
chmod       权限操作
tags: [linux,笔记,命令] #文章标签，可空，多标签请用格式，注意:后面有个空格
description: linux命令这么多我该怎么记-如何查找Linux的命令
---

## linux命令这么多我该怎么记-如何查找Linux的命令

https://linux.cn/lfs/LFS-BOOK-7.7-systemd/index.html

### 用户和组管理

```bash
chown       修改文件所有者(属主)
whoami      查看当前用户
useradd     创建用户
usermod -aG 群组 username 将用户加入群组，用逗号分隔
userdel -r username    删除用户
id [user]   查看用户的详细信息包括相关用户组
gpasswd -a [用户名] [组名] 将用户添加到组
groupdel [组名]         删除用户组
```

**find        查找**

> -name         名称
>   -maxdepth     递归层级(大)  
>   -mindepth     递归层级(小)  
>   -user         用户  
>   -group        属组  
>   -perm         权限  
>   -not          非(-not -user [name] #不是name用户,group等也可以组合)  
>   -exec         后接要执行的命令(-exec chmod o-w # 根据查找到的文件将其他人的权限改为不可写)  

```bash
free -m     查看内存的使用
uname -a    查看内核版本
locate      简单的查找文件
ldd     查看命令依赖
whereis     程序名搜索-b二进制文件-m man说明文件 -s源代码文件
which       搜索命令位置
nl          查看文件内容会显示行号
wc          统计文件信息
type        查看是不是shell自带命令
history     查看最近的所有命令可以陪grep使用，效果更好
alias       取别名
df -h       显示已经挂载的分区列表和磁盘使用情况
du -sh      查看目录占用空间
du -h       查看文件大小
sed 's/stringa1/stringa2/g' example.txt 替换命令，将example.txt文件中的 "string1" 替换成 "string2"
dump -0aj -f /tmp/home0.bak /home 制作一个 '/home' 目录的完整备份
nohup       使用nohup在登出ssh会话后仍继续运行命令
ranger      文件浏览
lsblk    查看磁盘挂载
kpartx -av  img文件不允许挂载时可先执行kpartx -av **.img后mount /dev/loop0 xxx
mkisofs     创建ISO镜像，-o 指定输出目录和文件名 例：mkiso -o /path/to/output.iso /path/to/www
uniq -u     显示唯一的行
uniq -d     显示重复行
comm        按行对比文件(并集，差集，交集)
```

**计划任务**

```bash
crontab -e  (* * * * * 用户 命令)
```

**内核模块管理**

```bash
/lib/modules/*/kernel    存放内核模块的目录 
lsmod       查看系统安装了哪些模块
# 内核模块的添加与删除
depmod      扫描新添加的模块
modprobe (name)     安装(name)模块
```

**进程管理**

```bash
kill pid    杀掉进程
```

**系统服务管理**

```bash
systemctl [start stop restart restartload]    启动,停止,重启,重载
systemctl status          显示系统启动状态
systemctl status (name)   查看启动状态
systemctl enable (name)   设为开机启动
systemctl disable (name)  禁用开机启动
systemctl is-enable (name)  查看是否开机启动
systemctl list-units      列出正在运行的单元
systemctl list-units -t service  列出有活动的服务
systemctl --failed        列出失败的单元
systemctl [start stop] firewalld   启动或关闭防火墙，firewalld为防火墙服务
systemctl help [单元]     显示单元手册页(如果单元支持)
跟操作界面相关
systemctl get-default     检查当前的默认启动目标
    graphical.target          文字加图形界面
    multi-user.target         纯文本模式
进入文本模式，反之由 multi-user 转 graphical
systemctl get-degault   查看默认模式，图形加文本为graphical
systemctl set-default multi-user.target 设置默认为文本模式
systemctl isolate multi-user.target     不重新开机的情况将操作环境改为纯文本模式
systemctl isolate graphical.target      进入图形界面
systemctl   电源
    poweroff    系统关机
    reboot      重新开机
    suspend     暂停模式
    hibernate   休眠模式
    rescue      强制进入救援模式
    emergency   强制进入紧急救援模式
跟踪目标间的依赖
systemctl list-dependencies         树状显示目前 target 环境下用到什么 unit
systemctl list-dependencies graphical.target        target 下用到什么 unit
systemctl list-dependencies [unit] --reverse    反向追踪谁会用到这个 unit
```

#### 系统日志

```bash
/var/log/message        核心系统日志文件,系统启动引导，运行状态，错误信息
/var/log/dmesg          核心启动日志，启动时会在屏幕显示与硬件有关的信息，
                        这些信息会保存在这个文件。
/var/log/auth.log 或 /var/log/secure
                        存储来自可插拔认证模块(PAM)的日志
/var/log/journal        systemd自己提供的日志系统，存放目录
journalctl              读取日志(systemd)
journalctl -b           本次启动的所有日志
journalctl -p err..alert      只显示错误冲突和重要告警信息
journalctl --vacuum-time=2weeks 清理两周前的日志，如果日志没有设置限定大小会越来，
                        这时候就需要手工清理
deesg                   显示系统的启动信息
last                    登陆记录
```

**卸载桌面环境**

```bash
ls /usr/share/xsessions/    确定需要卸载的桌面环境
sudo pacman -Rsc gnome      卸载gnome环境相关的软件包（包含配置文件和依赖包）
```

**暂停并在后台运行命令**

```bash
ctrl + z    暂停应用程序
bg          让其在后台运行
fg          重新将运用程序唤到前台
```
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

```bash
!!          重复上一条命令
c         重复上一条以ec开头的命令
!76         用命令历史(history)中的76号命令
```

**{}()语法**

```bash
touch name{1..10}.text
$(cmd)  #执行cmd在替换原来的命令
()  # 命令组括号中的命令会在开一个子shell执行
```
