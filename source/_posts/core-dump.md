---
title: Core Dumped(核心已转储)
date: 2024-08-06 13:55:10
tags: Linux
categories: Tools
---

# 1.生成core文件

设置core文件的大小限制和存储位置

-   设置core文件大小：`ulimit -c unlimited`

-   设置存储位置：

    ```
    sudo vim /etc/sysctl.conf
    kernel.core_pattern = /tmp/core-%p-%e-%t
    ```

    其本质是修改`/proc/sys/kernel/core_pattern`文件的内容，也可以使用其他方法

# 2.使用GDB来分析core文件

编译时加上`-g`选项，以便于生成的core文件可以用gdb来调试。例如：

```
gcc -g -o a a.c
./a
gdb ./a core-xx-xx
```

