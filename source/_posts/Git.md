---
title: Git
date: 2020-07-01 15:55:10
tags: Git
categories: Tools

---

## git rebase

假设一个项目有两个分支，一个是master，一个是dev，你在dev分支上正在开发一个新功能，但是这时候，有人已经在master分支上又有了新的提交，于是你的dev就落后了master一个commit，当你想把dev代码合到master时，需要这样做：
<!--more-->

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

## git reset

本地commit后发现提交进去了垃圾文件，或者commit的信息写错了，解决如下：
1、git reset --mixed HEAD^
使用 git reset HEAD^ 命令默认的就是mixed模式，此命令表示不删除本地工作空间提交的代码，也即保留对工作区的修改，但是修改未进入暂存区。

2、git reset --soft HEAD^
此命令也表示不删除本地工作空间提交的代码，也即保留对工作区的修改，并且修改已进入暂存区。

3、git reset --hard HEAD^
此命令表示删除本地工作空间提交的代码，也即不保留对工作区的修改，工作区完全回退到上个版本的样子。此命令注意慎用。

三者最大区别
前面两个命令会保留自己在本地的修改（纯撤回提交，如果是提交之后发现有的地方修改错误，可使用这两个命令撤回提交，然后只对错误的地方重新修改，最后再重新提交），而最后一个命令会恢复自己在本地的修改到上一个提交版本。

必备技能
1）HEAD^的意思是上一个版本，也可以写成HEAD～1，如果你进行了2次commit，都想撤回的话，可以使用HEAD～2，以此类推。
2）如果是commit注释写错了，只是想改一下注释，只需要执行命令行：git commit --amend。此时会进入默认Vim编辑器，修改完之后保存即可。
3）浪子回头再回头。意思是我撤回commit后，我又后悔了，我不想撤回了…。此时我们可以通过版本号来回退，先使用 git reflog 命令来获取版本号，再使用 git reset --hard 版本号 命令来恢复。