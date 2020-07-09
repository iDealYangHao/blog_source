---
title: File Compression
date: 2020-07-06 21:15:32
tags: Qt
categories: Qt

---

> 由于项目需要，我要将一个项目打包成deb文件，这是一种Linux下的安装包，deb包里有两个压缩文件，格式是`.tar.xz`,这是经过双重压缩的文件，本文主要讲压缩方法，附带讲Qt调用Terminal。

<!--more-->

# Qt调用Terminal

Qt中有个类：QProcess，很明显它是一个进程类，事实上Qt是新开了一个进程来进行bash操作，用法如下：

- 运行一条命令

```c++
QProcess p;
p.execute("ls -al");
```

- 运行很多条命令，即shell脚本

```C++
QProcess p;
p.execute("bash",QStringList()<<"-c"<<"/xxx/xxx.sh")
```

备注：p.execute和p.start的区别不在此赘述

# command line压缩文件

1. 先说压缩命令的格式: tar  -[参数]  xx.tar /xxx/xxx/xxx.txt

   1. tar是Ｌinux／Ｕnix下的一个命令，可以用 man tar　查看
   2. 参数是有很多的,常用的有x c v f等,x代表解压,c代表创建新压缩包,f表示文件名,v表示显示详细过程
   3. xx.tar表示你要压缩成什么名字
   4. /xxx/xxx/xxx.txt代表你想压缩的东西，可以是文件，也可以是文件夹
   5. 示例：ar -vcf yanghao.tar /home/yanghao/Desktop/test
   6. 两个注意点：
      1. f参数是必须的，且放在参数的最后一位
      2. 如果你的压缩名字指定了路径：/home/yanghao/yh.tar 那这个包再被解压的时候，就包含了/home/yanghao这个路径．所以建议在当前路径压缩

2. 然后xz yanghao.tar,就得到了 yanghao.tar.xz

3. 解压：tar -xf yanghao.tar.xz就直接解压了两层；

   如果你只想解压到tar这一层，那可以用xz -d yangaho.tar.xz，就生成了yanghao.tar

4. 其他压缩命令，待续...

