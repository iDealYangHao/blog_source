---
title: Unix文件操作
date: 2025-01-07 15:55:10
tags: File
categories: Unix

---

Unix下文件打开、关闭、读写、定位操作。这些函数属于不带缓冲的I/O，是POSIX.1的组成部分。
<!--more-->

## 一、打开文件

```c
#include <fcntl.h>

//若成功，返回文件描述符；若出错，返回−1
int open(const char *path, int oflag,... /* mode_t mode */);

```

-   path：要打开或者创建的文件名，相对路径、绝对路径都可以

-   oflag：打开方式：读、写、追加、创建等，主标志位必须且只能选择一个，副标志位可以多选或者不选，与主标志位进行或运算

    1.   主标志位

         1)   O_RDONLY　　　 只读打开

         2)   O_WRONLY　　　 只写打开

         3)   O_RDWR　　　　 读、写打开

              

         