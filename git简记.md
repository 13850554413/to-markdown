---
title: git笔记 #文章页面上的显示名称，一般是中文
date: 2018-10-07 15:30:16 #文章生成时间，一般不改，当然也可以任意修改
categories: 笔记 #分类
tags: [git,命令] #文章标签，可空，多标签请用格式，注意:后面有个空格
description: git命令快查
---

**创建仓库和提交**

    git init 把这个目录变成git可以管理的目录
    git add 添加到仓库
    git commit -m 提交到仓库
    git status 查看仓库当前的状态
    git diff 查看文件的变化

**版本回退**

注意：git之所以厉害是因为历史可回退和分支编辑，所以学好分支和版本回退是重中之重

    git log 查看提交日志
    git reset --hard HEAD^  回退到上一个版本(上上个版本HEAD^^)
    git reset --hard "commit id"    可以穿梭回去
    git checkout -- "file"  撤销修改/返回上次修改的状态add之前的状态
    git rm "file"   删除一个文件
    git push -u origin master 第一次推送
    git push 推送
    git remote add origin "仓库地址"  关联远程仓库
    git clone 克隆一个项目

**分支操作**

注意：git之所以厉害是因为历史可回退和分支编辑，所以学好分支和版本回退是重中之重

    git checout -b "新分支" 创建并切换到新分支
    git branch  查看当前分支
    git checkout "分支名称" 切换分支
    git merge "指定分支"    合并指定分支到当前分支
    git branch -d "分支名称"    删除分支
    git branch origin --delete dev
    git push origin :dev
    git log --graph 查看分支合并图

**更新的两种方法**

    git pull 直接拉取远程分支，简单但是把过程细节都隐藏了，一旦有问题很难找出错的地方
    git fetch 从另外一个仓库下载对象和引用
    git merge 合并

**远程操作**

    git clone [url] 克隆／下载
    git clone -b <branch> [url] 下载一个分支
    git branch --set-upstream-to=origin/develop 关联一个远程分支develop
    git remote -v 查看远程仓库信息  
    git remote add [name] [url] 添加远程仓库  
    git remote remove [name] 删除远程仓库name
    git fetch [name] 从name仓库更新同步代码
    git fetch -all 更新所有
    git merage --no-ff [name]/master 合并到本地代码
    git pull origin master 更新并合并自己远程仓库的代码
    git push -u 向自己的远程仓库推送刚才同步源仓库后的代码

**标签操作**

    git tag <tagname>   新建一个标签
    git tag -a <tanname> -m "aabbbcc...."   可以指定标签信息
    git tag 可以查看所有标签
    git push orgin <tagname> 推送一个本地标签
    git push orgin --tags 推送全部未推送过的标签
    git tag -d <tagname> 删除一个本地标签
    git push orgin :refs/tags/<tagname> 删除一个远程标签
    注意：删除文件需在执行一次 git rm 不然可能会有奇怪的情况
