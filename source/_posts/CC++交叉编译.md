---
title: C/C++交叉编译
date: 2024-011-11 15:55:10
tags: Cross Compile
categories: Tools
---

交叉编译区别于本地编译
<!--more-->

## 一、本地主机、目标主机和交叉编译

-   **本地主机**是完成开发、预处理、编译、汇编、链接的主机
-   **目标主机**是程序最终运行的主机，一般用于目标主机无法进行开发工作的情况，也适合用于多版本库的编译。
-   **交叉编译**是在本地主机编译能在目标主机运行的程序，本地主机和目标主机的指令集架构不同，一般是AMD64的本地和ARM的目标。

## 二、交叉编译工具

在本地主机开发，并在本地主机运行的叫本地编译，使用常规的本地编译器：gcc/g++。本地主机编译目标主机运行的叫交叉编译，需要使用对应的交叉编译工具，例如在x86_64（即AMD64）上编译arm（64位）架构的程序所需要安装的工具如下：

```shell
sudo apt install gcc-aarch64-linux-gnu  //安装c/c++交叉编译工具
sudo apt install g++-aarch64-linux-gnu

sudo apt install libc6-dev-arm64-cross  //编译时提醒缺少一些头文件
```

## 三、交叉编译程序

有如下c++程序, main.cpp:

```c++
#include <iostream>

using namespace std;

int main()
{
    cout << "g++ cross" << endl;
}
```

1.   本地编译，使用常规g++编译器

     ```shell
     g++ main.cpp    //编译，产生a.out的可执行文件
     ./a.out		    //运行，输出"g++ cross"
     ```

2.   使用交叉编译，需要使用刚下载的交叉编译工具

     ```shell
     //先查看交叉编译器工具版本，验证工具安装成功
     aarch64-linux-gnu-g++ -v
     
     //然后交叉编译上述main.cpp
     aarch64-linux-gnu-g++ main.cpp
     ```

     交叉编译出来的可执行文件不可以在本地主机运行，只能在符合的目标主机运行。所谓交叉编译，核心还是编译，把原本的`g++`换成`aarch64-linux-gnu-g++`即可。

## 四、进阶：使用cmake进行交叉编译

在CMakeLists.txt的同级目录下新建xxx.cmake文件，名字任意，后缀须为cmake，其内容如下：

```
# 指定目标系统
set(CMAKE_SYSTEM_NAME Linux)
# 指定目标平台
set(CMAKE_SYSTEM_PROCESSOR arm)
# 指定C编译器
set(CMAKE_C_COMPILER /usr/bin/aarch64-linux-gnu-gcc)
# 指定C++编译器
set(CMAKE_CXX_COMPILER /usr/bin/aarch64-linux-gnu-g++)
```

使用cmake时，需要加上该文件参数，指导cmake进行交叉编译：

```
//创建编译目录
mkdir build && cd build

//新建的xxx.cmake起名为：armToolchain.cmake
cmake .. -DCMAKE_TOOLCHAIN_FILE=../armToolchain.cmake

//进行编译
make
```

如果不带`-DCMAKE_TOOLCHAIN_FILE`参数，直接`cmake ..`就是进行本地编译

