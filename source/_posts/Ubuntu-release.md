---
title: Ubuntu的常用命令（五）发布程序
date: 2017-11-25 08:36:01
tags: linux
---
# release (pm2)

## pm2 
```bash
pm2 start [app]
```
## list all
```bash
pm2 list 
```
## [app] details
```bash
pm2 show [app]
```
## ecosystem.json
```json
{
  "apps" : [{
    "name"      : "blog",
    "script"    : "app.js",
    "env": {
      "COMMON_VARIABLE": "true"
    },
    "env_production" : {
      "NODE_ENV": "production"
    }
  }],
  "deploy" : {
    "production" : {
      "user" : "copy",
      "host" : ["192.168.1.98"],
	  "port" : "22",
      "ref"  : "origin/master",
      "repo" : "git@github.com:co-py/blog-api.git",
      "path" : "/var/www/blog/production",
      "ssh_options": "StrictHostKeyChecking=no",
      "pre-deploy-local" : "echo 'This is a local executed command'",
      "post-deploy" : "npm install --registry=https://registry.npm.taobao.org && pm2 startOrRestart ecosystem.json --env production",
      "env"  : {
        "NODE_ENV": "production"
      }
    }
  }
}

```

## deploy
```bash
# pm2 deploy <configuration_file> <environment> setup
pm2 deploy ecosystem.json production setup
```