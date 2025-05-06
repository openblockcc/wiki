---
title: 制作标准的资源图片
description: 
published: true
date: 2025-05-06T12:12:41.312Z
tags: 开发者
editor: markdown
dateCreated: 2024-07-18T05:41:06.628Z
---

# 制作标准的资源图片

OpenBlock 所有的官方资源的图片均遵循了一个标准，以此来保证界元素的统一性。

## 制作资源的主图 iconURL

这个图片用于在设备选择或扩展选择界面中显示，标准的图片参数如下。

- iconURL
	标准名称：[设备id]
	格式：png
	分辨率：600x372
	背景色：白色

同时要在图片周围留有指定宽度的空白边缘，可以直接下载下方图片在此基础上修改，将要添加的内容按比例缩放，居中放置并尽可能的填充中央的绿色部分，然后将背景色替换为白色即可。

- [standardimage.png](/developer-guide/plugin-development/create-standard-resource-images/standardimage.png)

![standardimage.png](/developer-guide/plugin-development/create-standard-resource-images/standardimage.png)

例如下方的图片。（灰色外框是示意内容，不存在于实际图片中）

![standardimagedemo.png](/developer-guide/plugin-development/create-standard-resource-images/standardimagedemo.png)

## 制作设备的 connectionIconURL 与 connectionSmallIconURL

这个图片用于在设备连接时的界面中显示。两张图片的参数分别如下

- connectionIconURL 
	标准名称：[设备id]-illustration
	格式：svg
  默认尺寸：108x87

- connectionSmallIconURL
	标准名称：[设备id]-small
	格式：svg
  默认尺寸：40x40

在制作这两张 `svg` 图片时，我们首先需要准备一个剔除了背景的设备图片，将图片尺寸调整为：`108 x 87px`，并将控制板居中，等比例缩放设备图片让它尽可能的填充整张图片，最后输出保存为一个背景透明的 `png` 格式的图片。然后我们再次调整图片长宽比为：`40 x 40px`，按照之前同样要求的调整并保存为一个新的 `png` 图片。

具体效果如下：

- [standarddeviceimagedemo108x87.png](/developer-guide/plugin-development/create-standard-resource-images/standarddeviceimagedemo108x87.png)

![standarddeviceimagedemo108x87.png](/developer-guide/plugin-development/create-standard-resource-images/standarddeviceimagedemo108x87.png)

- [standarddeviceimagedemo40x40.png](/developer-guide/plugin-development/create-standard-resource-images/standarddeviceimagedemo40x40.png)

![standarddeviceimagedemo40x40.png](/developer-guide/plugin-development/create-standard-resource-images/standarddeviceimagedemo40x40.png)

最后访问这个在线格式转换网站 [https://www.aconvert.com/image/](https://www.aconvert.com/image/)，将刚刚制作好的两张图片上传转换为 **SVG** 格式，将 **Resize image** 选项为 **Change width and height**，并分别设置为 `108x87` 和 `40x40`。执行转换完成后，右键 **OUTPUT FILE** 栏中的文件，选择 **链接另存为...** 下载他们，将 `108x87` 的图片命名为 `[设备id]-illustration`，`40x40` 的图片命名为 `[设备id]-small`。

具体文件如下:

- [standarddeviceimagedemo-illustration.svg](/developer-guide/plugin-development/create-standard-resource-images/standarddeviceimagedemo-illustration.svg)

![standarddeviceimagedemo-illustration.svg](/developer-guide/plugin-development/create-standard-resource-images/standarddeviceimagedemo-illustration.svg)

- [standarddeviceimagedemo-small.svg](/developer-guide/plugin-development/create-standard-resource-images/standarddeviceimagedemo-small.svg)

![standarddeviceimagedemo-small.svg](/developer-guide/plugin-development/create-standard-resource-images/standarddeviceimagedemo-small.svg)

> 用这个方法生成的 svg 图片实质上是内嵌了一个 png 图片的 svg 图片，并不是真正的矢量图，不过对于此处的用途来说是足够了。当然你也可以使用专业的矢量图编辑软件来制作他们。
{.is-info}





