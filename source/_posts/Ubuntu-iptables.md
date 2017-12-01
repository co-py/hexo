---
title: Ubuntu的常用命令（四）防火墻设置
date: 2017-11-24 22:30:59
tags: linux
---

# check rules
```bash
sudo  iptables -L
```
# clean rules
```bash 
sudo iptables -F
sudo iptables -X
```
# drop all 
```bash
# 关闭所有的 INPUT FORWARD OUTPUT 只对某些端口开放
iptables -P INPUT DROP
iptables -P FORWARD DROP
iptables -P OUTPUT DROP
```
# example
```bash
iptables -A INPUT -p tcp --dport 22 -j ACCEPT #ssh
iptables -A INPUT -p tcp --dport 80 -j ACCEPT #web
iptables -A INPUT -p tcp --dport 20 -j ACCEPT #FTP
iptables -A INPUT -p tcp --dport 21 -j ACCEPT
iptables -A INPUT -p tcp --dport 25 -j ACCEPT #email
iptables -A INPUT -p tcp --dport 110 -j ACCEPT
iptables -A OUTPUT -p tcp --sport 31337 -j DROP #hack
iptables -A OUTPUT -p tcp --dport 31337 -j DROP

```
# iptables config save 
```bash
su root
# 把设置的规则保存到指定的地方，文件名可以自定义
iptables-save >/etc/iptables.up.rules
# 调用Iptables设置
iptables-restore < /etc/iptables.up.rules
nano /etc/network/interfaces 
# gedit /etc/network/interfaces
在
auto ath0
     iface ath0 inet dhcp
	 后面，加上
pre-up iptables-restore >/etc/iptables.up.rules # 开机时自动调用已经存在的Iptables设置
post-down iptables-save >/etc/iptables.up.rules # 关机时自动保存当前的Iptables设置
```
# reload
```bash
iptables-restore < /etc/iptables.up.rules
```