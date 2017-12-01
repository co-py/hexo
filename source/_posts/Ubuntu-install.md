---
title: Ubuntu的常用命令（一）安装node环境
date: 2017-11-20 13:07:51
tags: linux
---
## Ubuntu 16.4

## init root

```bash
sudo passwd root
```

## change root

```bash
su root
```

## print where am i

```bash
pwd
```

## change home dir

```bash
cd ~
```
## add [user] to sudo
```bash
gpasswd -a copy sudo
sudo visudo
copy ALL=(ALL:ALL) ALL
```

# install soft

## apt-get install

```bash
su [username]
cd ~
sudo apt-get update
```
## install node env

```bash
sudo apt-get install curl
sudo curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.6/install.sh | bash
nvm -v
nvm install [node version] # v9.2.0
node -v
```

## npm change registry

```bash
npm -v
alias cnpm="npm --registry=https://registry.npm.taobao.org \
--cache=$HOME/.npm/.cache/cnpm \
--disturl=https://npm.taobao.org/dist \
--userconfig=$HOME/.cnpmrc"
cnpm -v
```

## install pm2

```bash
cnpm install -g pm2
pm2
```