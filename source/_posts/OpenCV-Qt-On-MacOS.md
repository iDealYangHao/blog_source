---
title: OpenCV & Qt On MacOS
date: 2020-06-20 20:42:31
tags: [Qt,OpenCV,macOS]
categories: 
	- [Qt]
	- [OpenCV]

---

> 初衷来源于我的毕业设计。当时导师要求做一个图像压缩算法的项目，要求有程序展示效果，但是我当时不会Qt，MFC也不会，就没法做一个可交互的界面了，强行用控制台交互...
>
> 现在正在从事于Qt开发，主要是用Qt开发UOS的桌面部件，但是我还是很喜欢OpenCV的，所以想把二者结合起来。为什么基于macOS，不谈。

<!-- more -->

# 一、安装Qt和OpenCV

​		网上都有教程，我假设你已经装好了，如果不会，请自行Google。值得一提的是OpenCV记得用` brew install opencv`来安装，具体原因未知（道听途说：手动编译的OpenCV就是添加不了动态库）。什么？不知道brew！？继续Google...

# 二、添加链接库

​		我们是在Qt Creator上开发的，你问我为什么不用Xcode？不好意思，我不会配置Qt跑在Xcode上，只会配置OpenCV的，所以我选择在Qt Creator上开发，添加OpenCV的库就行了。

​		在`.pro`文件中添加相关语句就行了。什么.pro?请关上电脑...主要有以下两个重点，只要添加好了，就可以成功运行你的Qt & OpenCv程序了。

## 1.添加头文件路径

`INCLUDEPATH  += /usr/local/Cellar/opencv/4.3.0_3/include`

​		请你别照抄，分析一下语句好吗？这个是你brew安装的Qt的路径，我们要添加include文件的里面的内容，这样就可以`#include <opencv2/opencv.hpp>`了。如果你是用brew安装的，那这个路径基本就是这样，找不到usr文件？请关机...这个地方有个大坑，路径原本应该是这样的`/4.3.0_3/opencv4/include`,但是我建议你删掉`opencv4`这一层目录，免得后面会报错（反正我处理不好..）。重中之重是include路径，不管你怎么安装的，只要找到了OpenCV的indlude就行了。

## 2.添加链接库

```cmake
LIBS += -L/usr/local/Cellar/opencv/4.3.0_3/lib \
    -lopencv_core \
    -lopencv_highgui \
    -lopencv_imgproc \
    -lopencv_imgcodecs \
    -lnumeric \
    -lopencv_features2d \
```

​		这个要注意 \ 前面是有空格的，另外路径，也请去找自己的路径，不要抄我的！`-L`和`-l`后面没有空格，`opencv_模块名`是一个个的链接库，不要加后缀，也不要加lib的前缀，为什么？我不知道...下面给一张图，再次强调一下inclue和lib。

![截屏2020-06-20 下午9.47.47](https://raw.githubusercontent.com/iDealYangHao/blogImages/master/%E6%88%AA%E5%B1%8F2020-06-20%20%E4%B8%8B%E5%8D%889.47.47.png)

​		最后给出一个源码，我也觉得各位一定迫不及待的地想要试试配置成功了没有，[拿去吧](https://github.com/iDealYangHao/Qt-OpenCV)!最后一句，一定要修改源码里面和你有关的部分...!