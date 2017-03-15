---
title: Python虚拟环境
date: 2017-03-15 13:33:26
tags:
  - Linux
  - Mac OS X
  - Python
---

玩过Python的朋友，往往都会安装有几个发行版本，主流是`Python2.x`和`Python3.x`。
如何切换运行环境的版本往往很麻烦，但是通过**virtualenv**一切又很简单了！

## virtualenv

### 文档

[官方-英文](https://virtualenv.pypa.io/en/stable/installation/)

### 安装

通过默认pip全局安装

```bash
$ [sudo] pip install virtualenv
```

### 使用

因为懒，所以这里建议安装 **virtualenvwrapper**。

**virtualenvwrapper** 是 **virtualenv** 的扩展管理包，
用于更方便管理虚拟环境。

## virtualenvwrapper

### 文档

[官方-英文](https://virtualenvwrapper.readthedocs.io/en/stable/install.html)

### 安装

1. 通过默认pip全局安装

    ```bash
    $ [sudo] pip install virtualenvwrapper
    ```

1. 在`~/.bashrc`中添加环境变量

    ```bash
    export WORKON_HOME=$HOME/.virtualenvs
    export PROJECT_HOME=$HOME/Devel
    export VIRTUALENVWRAPPER_SCRIPT=/usr/local/bin/virtualenvwrapper.sh
    source /usr/local/bin/virtualenvwrapper_lazy.sh
    ```

1. 编辑保存完后，运行`source ~/.bashrc`，使设置生效

### 使用

1. 可使用`virtualenvwrapper --help`查看所有命令方法

1. 但是常用就下面这几个

    * 创建环境：`mkvirtualenv` [环境名]
    * 删除环境：`rmvirtualenv` [环境名]
    * 激活环境：`workon` [环境名]
    * 退出环境：`deactivate`
    * 所有环境：`workon` / `lsvirtualenv -b`

### 事例

1. 例如当前环境安装有`Python2.7`和`Python3.5`，想自由切换`Python`运行环境

1. 先设置好虚拟环境

    ```bash
    mkvirtualenv -p /usr/bin/python2.7 env27 # env27就是你设置的环境名
    mkvirtualenv -p /usr/bin/python3.5 env35 # env35就是你设置的环境名
    ```

1. 列出所有虚拟环境，可以得到下面信息

    ```bash
    $ workon
    env27
    env35
    ```

1. 运行`workon env27`，就切换当前环境为`Python2.7`

1. 运行`workon env35`，就切换当前环境为`Python3.5`
