---
title: Shell脚本的提示输入
date: 2017-06-27 21:38:04
tags:
  - Linux
  - Shell
  - Bash
---

我们经常在shell脚本中会涉及交互输入，这里列举了一些`read`的常用脚本方便扩展。

## 原理

关于`read`命令的介绍可以看[Shell的read指令](https://windomz.github.io/2017/06/27/Shell%E7%9A%84read%E6%8C%87%E4%BB%A4/)

`read`是最常用的交互输入命令，并且shell基本都能支持。

## 用例

### 提示输入：
```bash
read -p "Do you understand this script? " content
```

### 提示输入密码：
```bash
read -s -p "Do you know what to enter? " password
echo "Success!"
```

### 提示输入：_是/否_

```bash
while true; do
  read -p "Do you understand this script?: [Y/n] " yn
  case ${yn} in
    [Yy]*|'' ) echo "YES!"; break;;
    [Nn]* ) echo "NO!"; break;;
    * ) echo "Please answer yes or no.";;
  esac
done
```
