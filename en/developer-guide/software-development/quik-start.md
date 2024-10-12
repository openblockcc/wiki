---
title: 快速开始
description: 
published: true
date: 2024-10-12T04:33:30.363Z
tags: 开发者
editor: markdown
dateCreated: 2024-07-17T02:38:01.983Z
---

# 快速开始
## 要求

请确保你的计算机已经安装好了以下软件或工具。

- Node.js 14/16（推荐使用16，过高或过低的 Node.js 版本均会导致在某些步骤编译失败）
- python2.7
- git
- node-gyp（同时根据 [node-gyp](https://github.com/nodejs/node-gyp?tab=readme-ov-file#installation) 官方说明安装必要的本地编译工具）

## 获取源代码并安装依赖包

1. 克隆工程的核心仓库。

```bash
mkdir openblock
cd openblock
git clone https://github.com/openblockcc/openblock-gui
git clone https://github.com/openblockcc/openblock-vm
git clone https://github.com/openblockcc/openblock-blocks
git clone https://github.com/openblockcc/openblock-link
git clone https://github.com/openblockcc/openblock-resource
```

2. 安装依赖并链接

```bash
cd openblock-blocks
npm install
npm link
cd ..
cd openblock-vm
npm install
npm link
cd ..
cd openblock-gui
npm install
npm link openblock-blocks openblock-vm
cd ..
```

`npm link` 指令会将本地 `npm` 包替换项目内默认的包，这样你在 `openblock-blocks` 等包中的修改才会被 `openblock-gui` 使用，否则它默认使用的将会是从 npm 服务器下载的内容，你可以通过查看 `openblock-gui/node_modules` 下的 `openblock-blocks` 与 `openblock-vm` 的文件夹来确认是否链接成功，如果成功那么他们将被链接到本工程的位置。

## 运行

1. 启动硬件接口服务器 openblock-link

```bash
cd openblock-link
npm start
```

2. 启动外部资源服务器 openblock-resource

在新的一个终端中执行。

```bash
cd openblock-resource
npm start
```

3. 启动 openblock-gui

在新的一个终端中执行。

```bash
cd openblock-gui
npm run start
```

在 openblock-gui 的 webpack 构建完成后，将会有弹出 openblock-gui 的网页，当然你也可以通过手动输入地址 http://127.0.0.1:8601/ 来访问。

> webpack 会持续监听工程内的源代码变动，包括链接到本地的软件包内的代码，也就意味着你在修改 openblock-gui 或是 openblock-vm 中的代码后只需要保存文件，就会触发 webpack 更新编译，这个过程的耗时要比重启 webpack 编译短很多，可以让我们方便的调试代码。
{.is-info}

> 但是对于 openblock-blocks 来说，由于其编译模式的特殊 (使用 google-closure-compiler 编译)，在修改其内部代码后我们不仅要在其路径下执行 npm run prepublish 重新编译代码，还需要重启 gui 的 webpack 服务器才能使变动生效。
{.is-warning}





