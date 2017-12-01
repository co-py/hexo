---
title: git的常用命令
date: 2017-11-22 08:36:01
tags: git
---

## generate key
```bash
mkdir .ssh
cd .ssh
ssh-keygen -t rsa -C "my.email@example.com" -b 4096
# iinux
chmod 0700 ~/.ssh
chmod 0600 ~/.ssh/id_rsa*
```
## copy key
```bash
cat ~/.ssh/id_rsa.pub
```
## Git Bash on Windows / Windows PowerShell
```bash 
cat ~/.ssh/id_rsa.pub | clip
```

## Git test
```bash 
ssh -T git@github.com
# Hi co-py You've successfully authenticated, but GitHub does not provide shell access.
```

## clone git res
```bash
git clone 'git@myproject.git'
```
## check status
```bash
git status -s
```
## commit
```bash
git init
git add .
git commit -m 'feat # init' 
git remote add origin 'git@myproject.git'
git push origin master

```
## reset
```bash
git reset -hard 'log.hash'
```
## error
```bash
ssh-agent bash
ssh-add id_rsa
# ssh: Could not resolve hostname ssh.github.com: Name or service not known
step1. ping github.com
step2. sudo nano /etc/hosts
	   add 192.30.252.128 github.com
```
