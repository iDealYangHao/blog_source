---
title: VS code with C/C++
date: 2020-07-05 16:59:01
tags: [macOS,VS code]
categories:
	- Tools
---

> VS code是一个跨平台的文本编辑器，当你给它加上各种插件后，它就会变成各种编译器，在各种平台，编译各种语言。本文就介绍C/C++在Win 10和macOS下的配置

<!--more-->

# VS code with Win 10

首先声明，MinGW是[Minimalist GNU for Windows](http://www.mingw.org), VS code只是一个文本编辑器，它不能编译程序，当它加上MinGW后，就成为了IDE。以下分两步走：

## 1.安装MinGW

这里有个详细教程：[知乎链接](https://zhuanlan.zhihu.com/p/66197013)。简单来说就是：

- 下载mingw-get-setup.exe，选择一个安装路径，比如：`C:\MinGW\`
- 添加系统变量，即Path中增加一个路径，是刚下载内容中的bin文件夹：`C:\MinGW\bin`

## 2.安装VS code，并配置环境

安装VS code略过。配置环境分两部分：

- **安装插件：C/C++（Microsoft维护的）、Code Runner（右上角的运行小三角）**

- **建立工作目录并设置两个json配置文件**

  假设你要写C++代码，我们就先建立一个文件夹：`C:\vs_cpp\`。进去了建立一个`.vscode`文件夹，然后在`.vscode`里面建立launch.json和task.json

- **写代码就在`.vscode`里面写**

```json
//launch.json
{
    "version": "0.2.0",
    "configurations": [{
        "name": "(gdb) Launch", // 配置名称，将会在启动配置的下拉菜单中显示
        "type": "cppdbg", // 配置类型，cppdbg对应cpptools提供的调试功能；可以认为此处只能是cppdbg
        "request": "launch", // 请求配置类型，可以为launch（启动）或attach（附加）
        "program": "${fileDirname}/${fileBasenameNoExtension}.exe", // 将要进行调试的程序的路径
        "args": [], // 程序调试时传递给程序的命令行参数，一般设为空即可
        "stopAtEntry": false, // 设为true时程序将暂停在程序入口处，相当于在main上打断点
        "cwd": "${workspaceFolder}", // 调试程序时的工作目录，此为工作区文件夹；改成${fileDirname}可变为文件所在目录
        "environment": [], // 环境变量
        "externalConsole": true, // 为true时使用单独的cmd窗口，与其它IDE一致；18年10月后设为false可调用VSC内置终端
        "internalConsoleOptions": "neverOpen", // 如果不设为neverOpen，调试时会跳到“调试控制台”选项卡，你应该不需要对gdb手动输命令吧？
        "MIMode": "gdb", // 指定连接的调试器，可以为gdb或lldb。但我没试过lldb
        "miDebuggerPath": "C:/mingw64/bin/gdb.exe", // 调试器路径，Windows下后缀不能省略，Linux下则不要
        "setupCommands": [
            { // 模板自带，好像可以更好地显示STL容器的内容，具体作用自行Google
                "description": "Enable pretty-printing for gdb",
                "text": "-enable-pretty-printing",
                "ignoreFailures": false
            }
        ],
        "preLaunchTask": "Compile" // 调试会话开始前执行的任务，一般为编译程序。与tasks.json的label相对应
    }]
}


//task.json
{
    "version": "2.0.0",
    "tasks": [{
        "label": "Compile", // 任务名称，与launch.json的preLaunchTask相对应
        "command": "g++",   // 要使用的编译器，C++用g++
        "args": [
            "${file}",
            "-o",    // 指定输出文件名，不加该参数则默认输出a.exe，Linux下默认a.out
            "${fileDirname}/${fileBasenameNoExtension}.exe",
            "-g",    // 生成和调试有关的信息
            "-Wall", // 开启额外警告
            "-static-libgcc",     // 静态链接libgcc，一般都会加上
            "-fexec-charset=GBK", // 生成的程序使用GBK编码，不加这一条会导致Win下输出中文乱码
            "-std=c11", // C++最新标准为c++17，或根据自己的需要进行修改
        ], // 编译的命令，其实相当于VSC帮你在终端中输了这些东西
        "type": "process", // process是vsc把预定义变量和转义解析后直接全部传给command；shell相当于先打开shell再输入命令，所以args还会经过shell再解析一遍
        "group": {
            "kind": "build",
            "isDefault": true // 不为true时ctrl shift B就要手动选择了
        },
        "presentation": {
            "echo": true,
            "reveal": "always", // 执行任务时是否跳转到终端面板，可以为always，silent，never。具体参见VSC的文档
            "focus": false,     // 设为true后可以使执行task时焦点聚集在终端，但对编译C/C++来说，设为true没有意义
            "panel": "shared"   // 不同的文件的编译信息共享一个终端面板
        },
        // "problemMatcher":"$gcc" // 此选项可以捕捉编译时终端里的报错信息；但因为有Lint，再开这个可能有双重报错
    }]
}
```

备注：`"miDebuggerPath": "C:/mingw64/bin/gdb.exe"`要改成你自己的路径

# VS code with macOS

假设你已经装过了Xcode

步骤很简单，如下：

- 安装两个插件：C/C++，code runner

- 新建一个文件夹A,在里面新建`.vscode`,然后进去新建两个json文件!

  ![](https://raw.githubusercontent.com/iDealYangHao/blogImages/master/截屏2020-07-05 下午6.49.13.png)

json文件如下：

```json
//launch.json
{
    "version": "0.2.0",
    "configurations": 
    [
        {
            "name": "(11db) Launch",
            "type": "cppdbg",
            "request": "launch",
            "program": "${workspaceRoot}/a.out",
            "args": [],
            "stopAtEntry": false,
            "cwd": "${workspaceFolder}",
            "environment": [],
            "externalConsole": true,
            "MIMode": "lldb"
        }
    ],
    // "compounds": []
}


//tasks.json
{
    "version": "2.0.0",
    "tasks": [
        {
            "label": "My Task",
            "command": "g++",
            "type": "shell",
            "args": [],
            "problemMatcher": [
                "$tsc"
            ],
            "presentation": {
                "reveal": "always"
            },
            "group": 
            {
                "kind": "build",
                "isDefault": true
            }
        }
    ],
}

```

备注：无需更改，task.json中command如果是c语言，就是gcc