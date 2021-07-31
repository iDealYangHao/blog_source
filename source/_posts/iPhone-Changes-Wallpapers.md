---
title: iPhone Changes Wallpapers
date: 2021-07-31 23:29:14
tags: [iPhone, unsplash]
categories: Tools
---

传统壁纸软件，有广告！很不爽！学会这个捷径，一键换iPhone壁纸。

<!--more-->

# shortcuts(捷径)设置壁纸

如图：设置流程，可以直接下载该[壁纸捷径](https://www.icloud.com/shortcuts/1acdcf04148441f1abf5307ce0b2028f)

![壁纸获取流程图](https://raw.githubusercontent.com/iDealYangHao/blogImages/master/20210731234308.jpg)

# Unsplash

这是一个开源图库，重点是**免费**！甚至你**商用**都可以，更甚至他们还开放了**接口**！[unsplash](https://unsplash.com), 就是这么良心.

## 获取任意图片

这是官方接口文档，仅对于低频获取的小型软件：https://source.unsplash.com ，还有一个针对开发者用户的：https://unsplash.com/developers ，开发者接口需要注册才可以使用。对于壁纸更换，用前一个就行了，无需注册，给出链接，直接下载图片。

```
//最简单，直接随机获取一张
https://source.unsplash.com/random
//加个尺寸
https://source.unsplash.com/random/800x600
//获取你喜欢的一个摄影师的作品（如果ta存在图库的话）
https://source.unsplash.com/user/erondu/1600x900
//获取你喜欢的摄影师喜欢的作品
https://source.unsplash.com/user/erondu/likes/1600x900
//获取非随机照片，daily或者weekly，每天/周只返回同一张图片
https://source.unsplash.com/daily
//获取包含某个对象的图片，比如自然主题类，里面还包含水的
https://source.unsplash.com/?nature,water
//你也可以找一张狗相关的图片，还带有具体尺寸，注意尺寸的位置不在最后了
https://source.unsplash.com/1600x900/?dog

//更详细的说明在官方
https://source.unsplash.com
```

将上述任意一个地址填到壁纸shortcuts的文本中，然后，run it！

对了，至于开发者才用到的接口，内容更加详细。但是我只是想换个壁纸呀～，后续如果在computer vision的学习中有需要大量图片，会专门看一下开发者接口的。其中一个场景就是：指定所有狗相关的图片，下载到本地，作为图片训练集，利用深度学习来让电脑认识“狗”。
