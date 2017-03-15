---
title: 管理切换多个Git账号
date: 2017-03-01 13:15:37
tags: 
  - Git
---

如何简单快捷在电脑管理和切换不同Git账号，诸如GitHub，GitLab等

## 前期准备

1. 安装[git](https://git-scm.com/downloads)，完成后`Windows`系统通过`git-bash`启动终端，
`Mac OS X`和`Linux`直接打开终端即可。

1. 拥有至少两个GitHub账号，例如有两个账号：`master`和`guest`。(下面内容均以GitHub账号为例)

1. 取消git全局设置

    ```bash
    git config --global --unset user.name
    git config --global --unset user.email
    ```

## SSH key配置

* [参考文档](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/)

1. 生成RSA公私秘钥

    ```bash
    ssh-keygen -t rsa -b 4096 -C "master_email@example.com"
    ```

1. 出现下列提示，可以输入秘钥的文件名（默认为`id_rsa`）

    ```markdown
    Enter a file in which to save the key (/Users/you/.ssh/id_rsa): [Press enter]
    ```

    例如`master`账号，可以输入`id_rsa_master`

1. 出现下列提示，是否需要绑定密码，可以选择不输入，即直接`ENTER`

    ```markdown
    Enter passphrase (empty for no passphrase): [Type a passphrase]
    Enter same passphrase again: [Type passphrase again]
    ```

1. 完成后在`~/.ssh/`目录就会生成私钥`id_rsa_master`和公钥`id_rsa_master.pub`

1. 添加SSH key

    ```bash
    ssh-add ~/.ssh/id_rsa_master
    ```

1. 通过下面命令，查看SSH key的设置

    ```bash
    ssh-add -l
    ```

1. `guest`账号的配置同上，得到私钥`id_rsa_guest`和公钥`id_rsa_guest.pub`

## GitHub账号配置

* [参考文档](https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/)

1. 登录`master`账号，在`Settings -> SSH and GPG keys`里，点击`New SSH key`

1. 在`"Title"`输入你要命名的名称，方便今后识别

1. 将公钥(`id_rsa_master.pub`)中的内容粘贴到`"Key"`中，可以通过下面命令打印内容

    ```bash
    cat ~/.ssh/id_rsa_master.pub
    ```

1. 点击`Add SSH key`按钮完成添加

1. `guest`账号的配置同上

## SSH config配置

1. 创建`config`文件

    ```bash
    cd ~/.ssh/
    touch config
    ```

1. 打开该`config`文件，写入以下内容保存:

    ```markdown
    # master(default)
    Host github.com
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_rsa_master
    
    # guest
    Host guest.github.com  # 这个可以任意设置
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_rsa_guest
    ```

1. 这里要说明下，今后相对应的SSH路径如下: 

    ```markdown
    # master(default)
    git@guest.github.com:master/your_repo.git
    
    # guest
    git@guest.github.com:guest/your_repo.git
    ```

## SSH测试

* [参考文档](https://help.github.com/articles/testing-your-ssh-connection/)

1. 测试`master`账号与GitHub的SSH连接

    ```bash
    ssh -T git@github.com
    ```

    成功会得到下面提示信息:

    ```markdown
    Hi <username>! You've successfully authenticated, but GitHub does not
    provide shell access.
    ```

1. 如果成功，在GitHub的`Settings -> SSH and GPG keys`里，相应的`SSH key`图标会变成绿色

1. `guest`账号的配置同上

## Git项目配置

1. 在Git项目中，例如`master`，命令行输入:

    ```bash
    git config user.name "master"
    git config user.email "master"
    ```

1. 查看Git项目的配置

    ```bash
    git config --list
    ```

1. 修改`git remote`:

    ```bash
    git remote rm origin
    git remote add origin git@github.com:master/your_repo.git
    ```

1. 如果是`guest`，修改`git remote`:

    ```bash
    git remote rm origin
    git remote add origin git@guest.github.com:guest/your_repo.git
    ```

1. 具体情况根据`~/.ssh/config`的配置内容调整相应URL

1. 完成后就可以愉快的`git pull`和`git push`了
