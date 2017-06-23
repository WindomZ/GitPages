---
title: Shell加载配置文件
date: 2017-06-23 23:27:50
tags:
  - Linux
  - Shell
  - Bash
---

在执行Shell命令时候，如何加载配置文件

## 原理

需把配置文件加载到环境变量(非全局)。

配置文件格式一般为`key=value`这种格式，
与`Shell`中的变量赋值相似，
如果在前面加上关键字`export`就可以声明为当前`Shell`的环境变量(非全局)

## 配置文件

假设一个配置文件`.env`，内容如下：
```text
Date=2009-01-03
Time=18:15:05
```

## 方法一

> 利用`sed`解析文本

```bash
date=`sed '/^Date=/!d;s/.*=//' .env`
time=`sed '/^Time=/!d;s/.*=//' .env`
echo $date
echo $time
```

## 方法二

> 利用`eval`方法解析

```bash
while read line;do
    eval "$line"
done < .env
echo $Date
echo $Time
```

## 方法三

> 利用`session`方法加载解析

打开终端
```bash
source .env
```
然后
```bash
echo $Date
echo $Time
```

## 测试

*方法一*和*方法二*可以在`Bash`脚本中运行，*方法三*只能在终端运行。

## 参考

[cnblogs](https://www.cnblogs.com/binbinjx/p/5680214.html)
