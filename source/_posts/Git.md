---
title: Git
date: 2020-07-01 15:55:10
tags: Git
categories: Tools

---

## git rebase

​        假设一个项目有两个分支，一个是master，一个是dev，你在dev分支上正在开发一个新功能，但是这时候，有人已经在master分支上又有了新的提交，于是你的dev就落后了master一个commit，当你想把dev代码合到master时，需要这样做：

```shell
git pull origin master --rebase
git push --force
```

**git commit --amend**

