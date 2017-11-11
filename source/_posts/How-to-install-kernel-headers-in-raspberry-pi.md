---
title: How to install kernel-headers in raspberry pi
date: 2017-11-11 21:38:04
tags:
  - Linux
  - raspbian
  - raspberry pi
---

## Issues

```
...
*** /lib/modules/4.9.59-v7+/build: No such file or directory.
```

Or

```
$ sudo apt-get install linux-headers-$(uname -r)
...
E: Unable to locate package linux-headers-4.9.59-v7
E: Couldn't find any package by glob 'linux-headers-4.9.59-v7'
E: Couldn't find any package by regex 'linux-headers-4.9.59-v7'
```

## Solution

Update
```bash
sudo apt-get update
```

Try
```bash
sudo apt-get install raspberrypi-kernel-headers
```

Done
```bash
sudo apt-get update && sudo apt-get upgrade
```
