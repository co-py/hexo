---
title: Ubuntu的常用命令（二）远程连接
date: 2017-11-21 12:07:51
tags: linux
---

## install openssh-server
```bash
sudo apt-get install openssh-server
```
## check ssh
```bash
dpkg -l | grep ssh
```

## check ps and print
```bash
ps -e | grep ssh #sshd
```

## start service
```bash
sudo service ssh start
```
---
## check ip
```bash
ifconfig
ifconfig th0 192.168.1.101
``` 