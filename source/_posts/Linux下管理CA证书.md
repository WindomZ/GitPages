---
title: Linux下管理CA证书(ca-certificates)
date: 2016-02-23 15:31:40
tags: 
  - Linux
  - CA
---

如何在Linux下管理CA证书，特别是排除某些颁发机构的证书

## 方案1：图形化配置CA证书

1. 打开终端，运行命令（需输入管理员密码）

    ```bash
    sudo dpkg-reconfigure ca-certificates
    ```

1. 在第一个显示图形化界面中，选择是否更新可信的新证书的证书颁发机构
(Trust new certificates from certificate authorities)，推荐选择**YES**

1. 在接下来界面中，是当前系统中的CA证书列表，可以上下移动光标，比如移动到CNNIC

    ```markdown
    [*] mozilla/CNNIC_ROOT.crt
    ```

1. CNNIC就不多说了，如果要清理证书，只需点击下空格键(`Space`)，变成

    ```markdown
    [ ] mozilla/CNNIC_ROOT.crt
    ```

1. 当然，下面这个也类似操作啦

    ```markdown
    [ ] mozilla/China_Internet_Network_Information_Center_EV_Certificates_Root.crt
    ```

1. 最后，按Tab键即可切换到**OK**，回车键(`Enter`)确定

## 方案2：文本化配置CA证书

1. 如果在Ubuntu下，打开终端，运行命令（需输入管理员密码）

    ```bash
    $ sudo gedit /etc/ca-certificates.conf
    或者
    $ sudo vim /etc/ca-certificates.conf
    ```

1. 将不需要的证书删除或者前面加**#**

1. 如果需要添加新增CA证书就新增一行

1. 保存退出

---

上面两个方案只是针对 Linux 且适用于 Chrome、Safari，其他浏览器如 Firefox、Opera 则需到浏览器设置里面进行配置

---

## 如何确认是否清楚CA证书？

用浏览器访问一下网站，地址是 https://www.cnnic.cn

如果浏览器报告该网站的证书有问题，那就OK啦
