---
title: OpenBlock编程棒开发者指南
description: 
published: true
date: 2024-10-12T04:19:28.468Z
tags: 
editor: markdown
dateCreated: 2023-10-16T10:31:37.883Z
---

# OpenBlock编程棒开发者指南

## 简介

OpenBlock 编程棒上搭载的是 OpenBlock Distro 版本，其外部资源插件系统的实现方式与桌面版构架是一样的。通过访问编程棒的 filebrowser 页面开发者可以自由的修改插件内容，以此来实现对编程棒软件内容的定制开发。

> 以下操作均建立在开发机与编程棒处于同一局域网的条件下，所以请先按照用户指南中的说明为编程棒完成网络配置。
{.is-info}

## 访问 filebrowser 页面

在浏览器中输入 `{ip}/filebrowser` 地址并打开即可打开 filebrowser 页面。

### 开发者目录文件介绍

- log 
	该为文件夹中存放编程棒中软件的工作日志，用于跟踪排查软件运行的错误。

- .cache
	等同于 OpenBlockDesktop 的缓存目录，用于存放编程生成的代码和构建，同时也是外部插件的缓存目录。

- firmwares
	与 OpenBlockDesktop 中的文件相同，存放使用的固件。
  
- external-resources
	与 OpenBlockDesktop 中的文件相同，存放外部插件和设备等扩展内容。

## 客制化开发

在上方的内容中我们已经了如何访问读取开发者账户的文件，也介绍了各个文件的功能，接下来我们来进行具体的开发步骤。

### 在桌面版中调试插件

编程棒中搭载的OpenBlock版本是完全兼容计算机版本上的外部资源文件的，由于编程棒的硬件资源受限，我们建议开发者先在计算机上使用常规的 OpenBlock 客制化开发方式即修改 external-resources 文件内容。

### 替换开发者目录下的 external-resources

在完成 external-resources 的修改后，使用直接替换掉编程棒开发者目录下的 `external-resources` 就可以让编程棒使用自己客制化开发的 external-resources 了。

### 重启编程棒并测试

**在上传完成后等待片刻（10秒左右，防止数据在内存中没有写入SD卡）**，而后我们重新启动编程棒，就可以刚刚修改的内容了。只要我们的插件在桌面版运行是没有问题的，那么按照上述方法替换编程棒中的 external-resources 后也一定不会有问题。
