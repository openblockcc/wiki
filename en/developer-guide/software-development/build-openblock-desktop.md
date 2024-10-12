---
title: 构建 OpenBlock Desktop
description: 
published: true
date: 2024-10-12T04:34:32.634Z
tags: 开发者
editor: markdown
dateCreated: 2024-07-18T08:21:26.909Z
---

# 构建 OpenBlock Desktop

## 准备工作

1. 首先获取桌面版源代码

```bash
git clone https://github.com/openblockcc/openblock-desktop
cd openblock-desktop
```

2. 安装依赖包

```bash
npm ci
```

## 运行与调试

编译代码并启动

```bash
cd openblock-desktop
npm run compile
npm run start
```

在 electron 启动后，我们可以使用以下快捷键打开网页控制台。

### Tab {.tabset}

#### Windows/Linux

<kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>i</kbd>

#### MacOS

<kbd>Command</kbd> + <kbd>Option</kbd> + <kbd>i</kbd>

### Tab {.tabset}

## 使用本地的依赖包

1. 切换 `openblock-gui` 分支并链接到本地的依赖包

注意在打包桌面版时，我们需要切换 `openblock-gui` 到 `desktop` 分支，该分支在处理一些静态图片等内容上相较 `main` 分支有所调整，以适配本地运行。如果在此之前你已经在 `develop` 分支下变动了代码，不要担心，使用 `git commit` 指令提交这些变更，并在切换到 `desktop` 分支后使用 `git merg` 指令合并即可。

```bash
git checkout desktop
npm link openblock-blocks openblock-vm
npm link
```

2. 在 `openblock-desktop` 中链接 `openblock-gui`

```bash
npm link openblock-gui
```

同样的如果你还有其他的本地软件包，也按照这样的方式链接即可。

## 打包

```bash
npm run dist
```

打包结束后就可以在 dist 文件夹下找到打包好的软件了。

> 如果你需要打包不同系统版本（如：MacOS，Linux）的软件，只要在不同系统下执行打包命令即可。
{.is-info}