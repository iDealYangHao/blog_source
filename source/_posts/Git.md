---
title: Git
date: 2020-07-01 15:55:10
tags: Git
categories: Tools

---

## git rebase

假设一个项目有两个分支，一个是master，一个是dev，你在dev分支上正在开发一个新功能，但是这时候，有人已经在master分支上又有了新的提交，于是你的dev就落后了master一个commit，当你想把dev代码合到master时，需要这样做：
<! --more-->
```shell
git pull origin master --rebase
git push --force
```

## git config

git可以进行一些配置,让git在使用的时候更顺手

```
//加了config代表全局都这样配置,不加代表只在本文件夹内这样配置
git config <--global> user.name "your name" 
git config <--global> user.email "your@email.com" 

//记住用户名和密码,执行完了这条命令后,git push推送时输入一次账号密码就可以记住了
git config <--global> credential.helper store
```
## git
