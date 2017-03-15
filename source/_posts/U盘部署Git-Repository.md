---
title: U盘部署Git仓库
date: 2016-01-25 15:08:05
tags: 
  - Git
---

如何简单快捷在U盘上部署Git仓库

## 准备
先把Git安装好，不然还玩什么Git
## U盘
1. 插上U盘，查看U盘的挂载路径
例如：U盘路径为“*/media/%user_name%/%usb_name%*”
``` bash
$ cd /media/%user_name%/%usb_name%
```

2. 创建一个用于仓库的文件夹，例如：起名为“*test.git*”
``` bash
$ mkdir test.git
$ cd test.git
```

3. 使用`--bare`创建的新仓库
``` bash
$ git init --bare
```

## 本机
1. 首先，有一个存在的项目（没有就创建一个或者文件夹），需要由Git接管版本控制，那么通过命令行来到这个项目目录，有一个项目的文件夹路径为“*~/Documents/MY_PROJECT*”
``` bash
$ cd ~/Documents/MY_PROJECT
```
    如果需要忽略某些文件，可以在此创建.gitignore文件，排除不需要的文件或者文件夹

2. 然后
``` bash
$ git init
```
    之后可以通过`git status`查看状态

3. 提交
``` bash
$ git add .
$ git commit -m "initialized"
```
    提交到了本地仓库

4. 例如：初始化名为“*usb*”的远程仓库
``` bash
$ git remote add usb /media/%user_name%/%usb_name%/test.git
```

5. 将本地仓库push到远程仓库usb上
``` bash
$ git push usb master
```

6. Pull的方式也类似
``` bash
$ git pull usb master
```