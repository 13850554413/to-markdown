---
title: pacman简记 #文章页面上的显示名称，一般是中文
date: 2023-11-02 15:30:16 #文章生成时间，一般不改，当然也可以任意修改
categories: 笔记 #分类
tags: [arch, pacman,笔记] #文章标签，可空，多标签请用格式，注意:后面有个空格
description: pacman常用命令
---

# 1. 第一部分使用 pacman-mirrors 更新官方软件源
## 1.1  按照地区自动更新为最快最稳定的软件源镜像地址

```bash
  sudo pacman-mirrors --country China
```

## 1.2. 恢复默认软件源操作

```bash
  sudo pacman-mirrors --interactive --default
```

## 1.3 软件源更新之后，我们一般会进行系统更新

```bash
$ sudo pacman -Syyu # 软件源更新完成之后进行系统软件更新操作
```

## 1.4 查看所有可用的地区信息

```bash
  sudo pacman-mirrors -l
```

____

# 2. 第二部分使用 pacman 管理软件
## 2.1 同步并且更新你的系统

```bash
  sudo pacman -Syu
```

## 2.2 在软件仓库中搜索软件

```bash
  sudo pacman -Ss [software package name]
```

## 2.3 查看已安装软件
```bash
  # 列出所有已安装的软件包
  pacman -Q
  # 搜索本地仓库的软件包
  sudo pacman -Qs [software package name]
```
## 2.4 查看软件的详细依赖

```bash
  sudo pactree [software package name]
```

## 2.5 查看系统中那些没有被使用软件依赖包（orphans）

```bash
  sudo pacman -Qdt
```

## 2.6 自动移除那些系统中没有被使用的依赖包【类似于Debian下的 sudo apt autoremove --purge】

```bash
  sudo pacman -Rs $(pacman -Qdtq)
```

## 2.7 下载并安装软件包

```bash
  pacman -Sw packge_name    # 下载但不安装它
  sudo pacman -Syu [software package name] # 从软件仓库安装
  yay -S [software package name]  # Packages from the AUR
  sudo pacman -U [/package_path/][software package name.pkg.tar.xz] # 从本地安装
  pacman -U http://www.examplepackage/repo/examplepkg.tar.xz # 从网络安装【非官方仓库】
```

## 2.8 卸载软件

```bash
  sudo pacman -R [software package name] 
  sudo pacman -Rs [software package name] # 同时删除依赖
  sudo pacman -Rns [software package name] # 删除软件及其依赖，还有pacman生成的配置文件，即更彻底的删除  
```

## 2.9 清空缓存【默认情况下安装软件会先来缓存中查看是否已经下载过，没有再去下载，软件安装后通常下载缓存还在】

```bash
  sudo pacman -Sc   # 删除目前没有安装的缓存包和没有被使用的同步数据库
  sudo pacman -Scc  # 删除所有缓存包（缓存文件夹）和没有被使用的同步数据库
  finished: 129 packages removed (disk space saved: 219.99 MiB)
  更加可控的清理软件包缓存可以用 paccache 命令，需要安装 pacman-contrib 包
  sudo paccache -r  # 保留最近3个版本的缓存，删除其他缓存包和已经卸载的软件包
  sudo paccache -rk[n]  # 指定保留 n 个版本的缓存，删除其他包和已卸载的包
  sudo paccache -ruk0   # 仅仅删除已卸载的包
  关于 pacman 常用就这些了，更多请使用 man pacman OR pacman -h 去查看
```

---

# 3.0 === 备份和恢复已安装软件包 ===

定期备份软件包是个好习惯。万一系统出了大问题，需要重装，就可以利用备份的软件包恢复到原先的系统。
*第一步，生成系统上安装的非本地（即从官方仓库获取的）软件包列表：*

```bash
$ comm -23 <(pacman -Qeq|sort) <(pacman -Qmq|sort) > pkglist
```

*把生成的pkglist存储在一个安全的地方，比如U盘，或者gist.github.com、evernote、dropbox之类的文本储存网站。
*今后重装系统时，把pkglist复制到新系统。
*使用如下命令安装所有软件包：

```bash
# pacman -S $(< pkglist)
```

要是备份的软件包列表包含非官方软件包（从AUR或其他什么地方下载的），就得使用下面这个吓人的命令了，不然pacman会出错：

```bash
# pacman -S --needed $(diff <(cat badpkglist|sort) <(diff <(cat badpkglist|sort) <(pacman -Slq|sort)|grep \<|cut -f2 -d' ')|grep \<|cut -f2 -d' ')
```

**解释：**

* ''pacman -Slq''列出所有可以安装的软件包。由于输出是按照来源仓库排序的，需要再调用''sort''排序。
* 排序是为''diff''命令比对列表做准备。
* 第一个''diff''返回所有无法安装的软件包；第二个返回所有可以安装的软件包。
* ''--needed''表示跳过已安装软件包。

可以接着用''yaourt''恢复从AUR获取的软件包（不推荐）：

```bash
$ yaourt -S --noconfirm $(diff <(cat badpkglist|sort) <(pacman -Slq|sort) |grep \<|cut -f2 -d' ')
```

最后，还可以卸载掉新系统上安装的、但之前系统并未安装的软件包。
**警告**:务必小心使用，仔细查看pacman输出，避免悲剧。

```bash
pacman -Rsu $(diff <(cat badpkglist|sort) <(pacman -Qq|sort) | grep \>|cut -f2 -d' ')
```

# 4.0 === 重新安装所有软件包 ===
要是你的系统遭到了大规模破坏（比如{{ic|rm -rf}}什么的），可以通过pacman重新安装所有软件包来挽救。
如果没有安装来自软件源外的软件包（比如来自AUR的），使用如下命令即可：
```bash
pacman -Qqn | pacman -S -
#pacman -S $(pacman -Qqn) # 如果上面的命令无法输入 y 以确认安装
```
如果安装了外来软件包，你可以使用 {{ic|pacman -Qqm}} 列出它们
# 5.0 其他
```bash
pacman -D --asdeps package-name     改变这个已安装包的原因为依赖，安装原因【（主动|显式）依赖】
            --asexplicit            附加选项，改变安装原因为显式
```
