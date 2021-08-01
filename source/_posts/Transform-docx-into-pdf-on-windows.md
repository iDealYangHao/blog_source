---
title: Transform docx into pdf on windows
date: 2021-08-01 20:26:05
tags: Qt
categories: Qt
---

在存在大批量docx文件转换为pdf文件时，使用word的转换功能，打开一个转换一个，要是让你转换100个呢？市面上迅捷转换器做的不错，但是一次只能转换200个文件，而且是会员情况下。要是你需要处理20万个docx文件呢？

<!--more-->

# 条件准备

windows 10电脑，装有word2016版及其以后，其他版本未测，情况未知。安装qt，如果你没有qt，可以现安装一个： https://download.qt.io/archive/qt/5.12/5.12.2/ ，具体细节从略。

![windows_qt](https://raw.githubusercontent.com/iDealYangHao/blogImages/master/20210801204028.png)

# 实现原理

Qt调用Microsoft的com组件，实现docx转换pdf操作，其实其他语言也可以调用这个com组件的，只不过Qt封装的比较好用。核心代码如下：

```C++
//新建一个word应用
QAxObject *wordApplication = new QAxObject("Word.Application");
//并设置为处理文档模式,因为word还可以处理非docx的文件
QAxObject *wordDoc = wordApplication>querySubObject("Documents");
//打开一个docx文件：inputfileName，比如：C:/Desktop/test.docx
QAxObject *doc = wordDoc>querySubObject("Open(string,bool,bool)",
  inputfileName,false, true);
//开始转换成pdf，OutputFileName由你自己决定,比如 C:/Desktop/test.pdf
doc->querySubObject("ExportAsFixedFormat(string, int ,bool)", 
  OutputFileName, 17, false);
//最后处理完毕了一定要把打开的docx文件给关闭了，不然处理太多了会卡死word
doc->dynamicCall("Close(bool)", false);
```

具体参数请看微软官方的文档： https://docs.microsoft.com/zh-CN/office/vba/api/Word.Documents.Open ，我不想啰里八嗦。

如果你连代码也不想写，拿去吧！pdf的代码仓库： https://github.com/iDealYangHao/word2pdf.git ,万一不能运行，可以gmail我。
